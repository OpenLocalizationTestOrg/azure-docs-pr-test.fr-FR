---
title: "aaaOperationalize intégré Spark apprentissage des modèles | Documents Microsoft"
description: "Mode tooload score les modèles de stockage et stockage des objets Blob Azure (WASB) avec Python."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="1f854-103">Faire fonctionner les modèles Machine Learning créés avec Spark</span><span class="sxs-lookup"><span data-stu-id="1f854-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="1f854-104">Cette rubrique montre comment toooperationalize un modèle d’apprentissage ordinateur enregistré (ML) à l’aide de Python sur HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="1f854-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="1f854-105">Il décrit comment les modèles d’apprentissage qui ont été générées à l’aide de Spark MLlib et stockées dans le stockage des objets Blob Azure (WASB) de l’ordinateur tooload et tooscore les jeux de données qui ont également été stockées dans WASB.</span><span class="sxs-lookup"><span data-stu-id="1f854-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="1f854-106">Il montre comment toopre à traiter les données d’entrée de hello, à l’aide des fonctionnalités de transformation hello des fonctions d’indexation et l’encodage dans hello MLlib toolkit, et comment toocreate un objet de données étiqueté point qui peut être utilisé comme entrée pour calculer les scores des modèles de hello ML.</span><span class="sxs-lookup"><span data-stu-id="1f854-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="1f854-107">les modèles de Hello utilisés pour calculer les scores incluent la régression linéaire, régression logistique, les modèles de forêt aléatoire et modèles d’arbre de Gradient Boosting.</span><span class="sxs-lookup"><span data-stu-id="1f854-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="1f854-108">Clusters Spark et notebooks Jupyter</span><span class="sxs-lookup"><span data-stu-id="1f854-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="1f854-109">Étapes de configuration et toooperationalize de code hello un modèle ML sont fournies dans cette procédure pas à pas pour l’utilisation d’un cluster HDInsight Spark 1.6 ainsi que d’un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="1f854-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="1f854-110">code Hello de ces procédures est également fourni dans les blocs-notes Notebook.</span><span class="sxs-lookup"><span data-stu-id="1f854-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="1f854-111">Notebook pour Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="1f854-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="1f854-112">Hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) bloc-notes jupyter montre comment toooperationalize un modèle enregistré à l’aide de Python sur HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="1f854-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="1f854-113">Notebook pour Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="1f854-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="1f854-114">toomodify hello notebook ordinateur portable pour toouse Spark 1.6 avec un cluster HDInsight Spark 2.0, remplacez le fichier de code Python hello avec [ce fichier](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="1f854-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="1f854-115">Ce code montre comment les modèles de hello tooconsume créés dans Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="1f854-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1f854-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f854-116">Prerequisites</span></span>

1. <span data-ttu-id="1f854-117">Vous avez besoin d’un compte Azure et un Spark 1.6 (ou Spark 2.0) du cluster HDInsight toocomplete cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="1f854-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="1f854-118">Consultez hello [vue d’ensemble de science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md) pour obtenir des instructions sur la façon de toosatisfy ces exigences.</span><span class="sxs-lookup"><span data-stu-id="1f854-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="1f854-119">Cette rubrique contient également une description de type hello données NYC 2013 Taxi utilisées ici et obtenir des instructions sur la façon dont tooexecute code à partir d’un bloc-notes jupyter sur cluster Spark de hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="1f854-120">Vous devez également créer hello modèles d’apprentissage automatique toobe notées ici en passant par hello [exploration de données et modélisation avec Spark](machine-learning-data-science-spark-data-exploration-modeling.md) rubrique pour le cluster de hello Spark 1.6 ou les blocs-notes hello Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="1f854-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="1f854-121">les blocs-notes Hello Spark 2.0 utilisent un jeu de données supplémentaire pour tâche de classification hello, hello connu compagnie aérienne à temps départ dataset à partir de 2011 et 2012.</span><span class="sxs-lookup"><span data-stu-id="1f854-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="1f854-122">Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent.</span><span class="sxs-lookup"><span data-stu-id="1f854-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="1f854-123">En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="1f854-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="1f854-124">Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="1f854-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="1f854-125">Le programme d’installation : hello, les bibliothèques et les emplacements de stockage prédéfinir le contexte de Spark</span><span class="sxs-lookup"><span data-stu-id="1f854-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="1f854-126">Spark est en mesure de tooan de tooread et écriture objet Blob de stockage Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="1f854-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="1f854-127">Par conséquent, vos données existantes qui y sont stockées peuvent être traitées à l’aide de Spark et hello stockées dans WASB des résultats.</span><span class="sxs-lookup"><span data-stu-id="1f854-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="1f854-128">toosave modèles ou les fichiers dans WASB, chemin d’accès hello doit toobe correctement spécifiée.</span><span class="sxs-lookup"><span data-stu-id="1f854-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="1f854-129">Hello du cluster Spark toohello conteneur attaché par défaut peut être référencé à l’aide d’un chemin commençant par : *« wasb / / »*.</span><span class="sxs-lookup"><span data-stu-id="1f854-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="1f854-130">exemple de code suivant Hello spécifie emplacement hello de hello toobe de données en lecture et chemin d’accès de hello pour hello modèle stockage toowhich hello modèle de sortie est enregistré.</span><span class="sxs-lookup"><span data-stu-id="1f854-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="1f854-131">Définir les chemins d’accès aux emplacements de stockage dans WASB</span><span class="sxs-lookup"><span data-stu-id="1f854-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="1f854-132">Les modèles sont enregistrés dans : wasb:///user/remoteuser/NYCTaxi/Models.</span><span class="sxs-lookup"><span data-stu-id="1f854-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="1f854-133">Si ce chemin d’accès n’est pas défini correctement, les modèles ne sont pas chargés en vue de leur notation.</span><span class="sxs-lookup"><span data-stu-id="1f854-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="1f854-134">Hello score résultats ont été enregistrés dans : « wasb : / / / utilisateur/UtilisateurDistant/NYCTaxi/ScoredResults ».</span><span class="sxs-lookup"><span data-stu-id="1f854-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="1f854-135">Si toofolder de chemin d’accès hello est incorrecte, les résultats ne sont pas enregistrés dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="1f854-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="1f854-136">emplacements de chemin d’accès de fichier Hello peuvent être copiés et collés dans des espaces réservés de hello dans ce code de sortie de hello de hello dernière cellule de hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1f854-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="1f854-137">Voici les chemins d’accès du répertoire tooset code hello :</span><span class="sxs-lookup"><span data-stu-id="1f854-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="1f854-138">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-138">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="1f854-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="1f854-140">Importer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="1f854-140">Import libraries</span></span>
<span data-ttu-id="1f854-141">Définir le contexte de spark et importer des bibliothèques nécessaires avec hello suivant de code</span><span class="sxs-lookup"><span data-stu-id="1f854-141">Set spark context and import necessary libraries with hello following code</span></span>

    #IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="1f854-142">Contexte Spark prédéfini et commandes magiques PySpark</span><span class="sxs-lookup"><span data-stu-id="1f854-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="1f854-143">noyaux PySpark Hello qui sont fournis avec les ordinateurs portables Notebook ont un contexte prédéfini.</span><span class="sxs-lookup"><span data-stu-id="1f854-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="1f854-144">Par conséquent, il est inutile tooset hello Spark ou ruche contextes explicitement avant de commencer à utiliser avec l’application hello que vous développez.</span><span class="sxs-lookup"><span data-stu-id="1f854-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="1f854-145">Ils sont disponibles pour vous par défaut.</span><span class="sxs-lookup"><span data-stu-id="1f854-145">These are available for you by default.</span></span> <span data-ttu-id="1f854-146">Ces contextes sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="1f854-146">These contexts are:</span></span>

* <span data-ttu-id="1f854-147">sc : pour Spark</span><span class="sxs-lookup"><span data-stu-id="1f854-147">sc - for Spark</span></span> 
* <span data-ttu-id="1f854-148">sqlContext : pour Hive</span><span class="sxs-lookup"><span data-stu-id="1f854-148">sqlContext - for Hive</span></span>

<span data-ttu-id="1f854-149">Hello PySpark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec %%.</span><span class="sxs-lookup"><span data-stu-id="1f854-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="1f854-150">Deux de ces commandes sont utilisées dans ces exemples de code.</span><span class="sxs-lookup"><span data-stu-id="1f854-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="1f854-151">**%% local** spécifié que le code hello dans les lignes suivantes est exécuté localement.</span><span class="sxs-lookup"><span data-stu-id="1f854-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="1f854-152">Le code doit être du code Python valide.</span><span class="sxs-lookup"><span data-stu-id="1f854-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="1f854-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="1f854-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="1f854-154">Exécute une requête Hive sur hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="1f854-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="1f854-155">Si le paramètre -o de hello est transmis, résultat hello de requête de hello est conservé dans hello %% contexte Python local en tant qu’une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="1f854-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="1f854-156">Pour plus d’informations sur les noyaux hello pour notebook blocs-notes et hello prédéfinies « magics » qui elles fournissent, consultez [clusters de noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="1f854-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="1f854-157">Recevoir les données et créer une trame de données nettoyée</span><span class="sxs-lookup"><span data-stu-id="1f854-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="1f854-158">Cette section contient le code hello pour une série de tâches requise tooingest hello données toobe transformée.</span><span class="sxs-lookup"><span data-stu-id="1f854-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="1f854-159">Lire dans un exemple de 0,1 % jointes de hello taxi voyage et tarif de fichier (stocké sous la forme d’un fichier .tsv), des données au format hello et crée ensuite une trame de données propre.</span><span class="sxs-lookup"><span data-stu-id="1f854-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="1f854-160">Hello taxi voyage et tarif les fichiers ont été joints en fonction de procédure hello fourni dans le : [hello du processus de science des données équipe en action : à l’aide de clusters HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="1f854-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1f854-161">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-161">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-162">Temps nécessaire tooexecute au-dessus de la cellule : 46.37 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="1f854-163">Préparer les données à la notation dans Spark</span><span class="sxs-lookup"><span data-stu-id="1f854-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="1f854-164">Cette section montre comment tooindex, coder et mettre à l’échelle tooprepare fonctionnalités catégorielles pour utilisent dans les algorithmes d’apprentissage automatique de MLlib contrôlé pour la classification et de régression.</span><span class="sxs-lookup"><span data-stu-id="1f854-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="1f854-165">Transformation de caractéristiques : indexer et encoder des caractéristiques catégorielles en vue de leur utilisation dans des modèles à noter</span><span class="sxs-lookup"><span data-stu-id="1f854-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="1f854-166">Cette section montre comment à l’aide des données catégorielles tooindex un `StringIndexer` et coder les fonctionnalités avec `OneHotEncoder` d’entrée dans les modèles hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="1f854-167">Hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encode une colonne de chaîne de la colonne d’étiquettes de tooa d’index de l’étiquette.</span><span class="sxs-lookup"><span data-stu-id="1f854-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="1f854-168">indices de Hello sont classés par fréquence d’étiquette.</span><span class="sxs-lookup"><span data-stu-id="1f854-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="1f854-169">Hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mappe une colonne de la colonne de tooa étiquette indices de vecteurs binaire, au maximum une seule une valeur.</span><span class="sxs-lookup"><span data-stu-id="1f854-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="1f854-170">Cet encodage permet d’algorithmes qui attendent des fonctionnalités à valeurs continues, telles que la régression logistique, fonctionnalités de toocategorical toobe appliqué.</span><span class="sxs-lookup"><span data-stu-id="1f854-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1f854-171">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-171">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-172">Temps nécessaire tooexecute au-dessus de la cellule : 5.37 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="1f854-173">Créer des objets RDD avec des tableaux de caractéristiques à intégrer dans des modèles</span><span class="sxs-lookup"><span data-stu-id="1f854-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="1f854-174">Cette section contient le code qui montre comment les données de texte catégorielles tooindex comme un RDD de l’objet et à chaud de celui Encoder donc il peut être utilisé tootrain et test MLlib régression logistique et les modèles basés sur l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="1f854-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="1f854-175">les données indexées Hello sont stockées dans [résilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objets.</span><span class="sxs-lookup"><span data-stu-id="1f854-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="1f854-176">Il s’agit d’abstraction de base hello dans Spark.</span><span class="sxs-lookup"><span data-stu-id="1f854-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="1f854-177">Un objet RDD représente une collection immuable et partitionnée d’éléments qui peuvent faire l’objet d’un traitement en parallèle avec Spark.</span><span class="sxs-lookup"><span data-stu-id="1f854-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="1f854-178">Il contient également le code qui montre comment les données tooscale avec hello `StandardScalar` fournie par MLlib pour une utilisation dans la régression linéaire avec stochastique dégradé descente (SGD), un algorithme populaire pour l’apprentissage d’un large éventail de modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="1f854-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="1f854-179">Hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale utilisé hello fonctionnalités toounit écart.</span><span class="sxs-lookup"><span data-stu-id="1f854-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="1f854-180">Fonctionnalité mise à l’échelle, également appelé normalisation des données, ainsi que des fonctionnalités avec des valeurs largement dispersées sont pas donné excessive peser en fonction de l’objectif hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1f854-181">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-181">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-182">Temps nécessaire tooexecute au-dessus de la cellule : 11.72 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="1f854-183">Score avec hello modèle de régression logistique et enregistrer la sortie tooblob</span><span class="sxs-lookup"><span data-stu-id="1f854-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="1f854-184">code Hello dans cette section explique comment tooload un modèle de régression logistique qui a été enregistré dans Azure stockage d’objets blob et utiliser toopredict ou non une info-bulle est payée sur un voyage taxi, il score avec les mesures de classification standard et puis enregistrez et tracer hello résultats tooblob stockage.</span><span class="sxs-lookup"><span data-stu-id="1f854-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="1f854-185">Hello résultats évalué sont stockées dans les objets RDD.</span><span class="sxs-lookup"><span data-stu-id="1f854-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="1f854-186">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-186">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-187">Temps nécessaire tooexecute au-dessus de la cellule : 19.22 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="1f854-188">Noter un modèle de régression linéaire</span><span class="sxs-lookup"><span data-stu-id="1f854-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="1f854-189">Nous avons utilisé [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) payé de tootrain un modèle de régression linéaire à l’aide de descente de Gradient stochastique (SGD) toopredict hello pendant l’optimisation d’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="1f854-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="1f854-190">code Hello dans cette section explique comment les tooload un modèle de régression linéaire à partir du stockage d’objets blob Azure, score à l’aide de variables à l’échelle et puis enregistrez les objets blob de hello résultats toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="1f854-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1f854-191">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-191">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-192">Temps nécessaire tooexecute au-dessus de la cellule : 16.63 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="1f854-193">Noter les modèles Forêts aléatoires de classification et de régression</span><span class="sxs-lookup"><span data-stu-id="1f854-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="1f854-194">code Hello dans cette section montre comment les hello tooload enregistrées classification et les modèles forêt aléatoire de régression, enregistré dans le stockage d’objets blob Azure, un score de leurs performances avec classifieur standard et les mesures de régression, puis enregistrez hello résultats précédent tooblob stockage.</span><span class="sxs-lookup"><span data-stu-id="1f854-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="1f854-195">[forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="1f854-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="1f854-196">Combiner des nombreux decision trees tooreduce hello des risques de dépassement de.</span><span class="sxs-lookup"><span data-stu-id="1f854-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="1f854-197">Forêts aléatoires peuvent gérer les fonctionnalités catégorielles, étendre les paramètre de classification multiclasse toohello, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1f854-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="1f854-198">Forêts aléatoires sont un des hello plus de succès d’apprentissage des modèles pour la classification et la régression.</span><span class="sxs-lookup"><span data-stu-id="1f854-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="1f854-199">[spark.mllib](http://spark.apache.org/mllib/) prend en charge les forêts aléatoires pour la classification binaire et multiclasse et pour la régression, à l’aide des caractéristiques continues et catégorielles.</span><span class="sxs-lookup"><span data-stu-id="1f854-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="1f854-200">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-200">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-201">Temps nécessaire tooexecute au-dessus de la cellule : 31.07 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="1f854-202">Noter les modèles GBT de classification et de régression</span><span class="sxs-lookup"><span data-stu-id="1f854-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="1f854-203">code Hello dans cette section montre comment classification de tooload et de régression des modèles d’arbre de Gradient Boosting à partir du stockage d’objets blob Azure, un score de leurs performances avec classifieur standard et les mesures de régression, puis enregistrez hello résultats précédent tooblob stockage.</span><span class="sxs-lookup"><span data-stu-id="1f854-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="1f854-204">**spark.mllib** prend en charge les arbres GBT pour la classification binaire et la régression, à l’aide des caractéristiques continues et catégorielles.</span><span class="sxs-lookup"><span data-stu-id="1f854-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="1f854-205">[Gradient Boosted Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="1f854-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="1f854-206">Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte.</span><span class="sxs-lookup"><span data-stu-id="1f854-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="1f854-207">GBTs peut gérer les fonctionnalités catégorielles, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1f854-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="1f854-208">Ils s’utilisent également dans le paramétrage de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="1f854-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1f854-209">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-209">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-210">Temps nécessaire tooexecute au-dessus de la cellule : 14.6 secondes</span><span class="sxs-lookup"><span data-stu-id="1f854-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="1f854-211">Nettoyer des objets de la mémoire et imprimer les emplacements de fichier notés</span><span class="sxs-lookup"><span data-stu-id="1f854-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="1f854-212">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1f854-212">**OUTPUT:**</span></span>

<span data-ttu-id="1f854-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="1f854-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="1f854-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="1f854-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="1f854-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="1f854-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="1f854-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="1f854-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="1f854-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="1f854-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="1f854-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="1f854-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="1f854-219">Utiliser les modèles Spark via une interface web</span><span class="sxs-lookup"><span data-stu-id="1f854-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="1f854-220">Spark fournit un mécanisme tooremotely submit traitements ou requêtes interactives via un reste de l’interface avec un composant appelé Livy.</span><span class="sxs-lookup"><span data-stu-id="1f854-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="1f854-221">Par défaut, Livy est activé sur votre cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1f854-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="1f854-222">Pour plus d’informations sur Livy, consultez [Envoi de travaux Spark à distance en utilisant Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="1f854-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="1f854-223">Vous pouvez utiliser Livy tooremotely soumettre un travail qui par lots scores un fichier qui est stocké dans un objet blob Azure, puis écrit blob de tooanother résultats hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="1f854-224">toodo, vous téléchargez le script Python hello</span><span class="sxs-lookup"><span data-stu-id="1f854-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="1f854-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) blob toohello de cluster de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="1f854-226">Vous pouvez utiliser un outil tel que **Microsoft Azure Storage Explorer** ou **AzCopy** le blob cluster toohello toocopy hello script.</span><span class="sxs-lookup"><span data-stu-id="1f854-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="1f854-227">Dans notre cas, nous avons téléchargé script de hello trop***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="1f854-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="1f854-228">Bonjour les touches d’accès rapide qui vous avez besoin se trouvent sur le portail de compte de stockage hello associé hello Spark cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="1f854-229">Une fois téléchargé toothis emplacement, ce script s’exécute dans un cluster Spark de hello dans un contexte distribué.</span><span class="sxs-lookup"><span data-stu-id="1f854-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="1f854-230">Il charge le modèle de hello et exécute des prédictions sur les fichiers d’entrée en fonction de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1f854-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="1f854-231">Vous pouvez exécuter ce script à distance en effectuant une simple requête HTTPS/REST sur Livy.</span><span class="sxs-lookup"><span data-stu-id="1f854-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="1f854-232">Voici un curl commande tooconstruct hello HTTP demande tooinvoke hello script Python à distance.</span><span class="sxs-lookup"><span data-stu-id="1f854-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="1f854-233">Remplacez les valeurs appropriées hello pour votre cluster Spark CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME.</span><span class="sxs-lookup"><span data-stu-id="1f854-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="1f854-234">Vous pouvez utiliser n’importe quel langage sur hello distant tooinvoke hello Spark tâche système via Livy en effectuant un simple appel HTTPS avec l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="1f854-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="1f854-235">Il serait bibliothèque de demandes de Python hello toouse pratique lors de l’établissement de cet appel HTTP, mais il n’est pas installé par défaut dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1f854-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="1f854-236">C’est pourquoi les anciennes bibliothèques HTTP sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="1f854-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="1f854-237">Voici le code Python de hello pour l’appel de hello HTTP :</span><span class="sxs-lookup"><span data-stu-id="1f854-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="1f854-238">Vous pouvez également ajouter ce code Python trop[Azure fonctions](https://azure.microsoft.com/documentation/services/functions/) tootrigger une soumission de travaux Spark qui évalue un objet blob en fonction de divers événements comme un minuteur, la création ou la mise à jour d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="1f854-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="1f854-239">Si vous préférez une expérience client libre de code, utilisez hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark score par lot en définissant une action HTTP sur hello **Concepteur d’applications logique** et en définissant ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="1f854-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="1f854-240">Sur le portail Azure, créez une application logique en sélectionnant **+Nouveau** -> **Web + Mobile** -> **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="1f854-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="1f854-241">toobring des hello **Concepteur d’applications logique**, entrez le nom hello hello logique d’application et le Plan App Service.</span><span class="sxs-lookup"><span data-stu-id="1f854-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="1f854-242">Sélectionnez une action HTTP et entrez des paramètres de hello illustrés hello figure suivante :</span><span class="sxs-lookup"><span data-stu-id="1f854-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Concepteur Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="1f854-244">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="1f854-244">What's next?</span></span>
<span data-ttu-id="1f854-245">**Validation croisée et balayage hyperparamétrique**: consultez [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment effectuer la formation des modèles à l’aide de la validation croisée et du balayage hyperparamétrique.</span><span class="sxs-lookup"><span data-stu-id="1f854-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

