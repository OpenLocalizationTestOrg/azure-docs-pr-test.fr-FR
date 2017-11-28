---
title: "Faire fonctionner les modèles Machine Learning créés avec Spark | Microsoft Docs"
description: "Comment charger et noter les modèles d’apprentissage stockés dans Azure Blob Storage (WASB) avec Python."
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
ms.openlocfilehash: 00fec675bed0137473f7e3c5ddfe9c3c0e8344c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="e7462-103">Faire fonctionner les modèles Machine Learning créés avec Spark</span><span class="sxs-lookup"><span data-stu-id="e7462-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="e7462-104">Cette rubrique montre comment faire fonctionner un modèle Machine Learning (ML) à l’aide de Python sur des clusters HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-104">This topic shows how to operationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="e7462-105">Elle décrit comment charger des modèles Machine Learning créés avec Spark MLlib et stockés dans Azure Blob Storage (WASB), et explique comment les noter avec des jeux de données également stockés dans WASB.</span><span class="sxs-lookup"><span data-stu-id="e7462-105">It describes how to load machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how to score them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="e7462-106">Il montre comment prétraiter les données d’entrée, transformer les caractéristiques à l’aide des fonctions d’indexation et d’encodage du kit d’outils MLlib, et comment créer un objet de données point étiqueté, utilisable comme entrée de notation avec les modèles ML.</span><span class="sxs-lookup"><span data-stu-id="e7462-106">It shows how to pre-process the input data, transform features using the indexing and encoding functions in the MLlib toolkit, and how to create a labeled point data object that can be used as input for scoring with the ML models.</span></span> <span data-ttu-id="e7462-107">Les modèles utilisés pour la notation sont les suivants : Régression linéaire, Régression logistique, Modèles de forêts aléatoires et Modèles GBT (Gradient Boosting Tree).</span><span class="sxs-lookup"><span data-stu-id="e7462-107">The models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="e7462-108">Clusters Spark et notebooks Jupyter</span><span class="sxs-lookup"><span data-stu-id="e7462-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="e7462-109">Cette procédure pas à pas fournit les étapes d’installation et le code permettant de faire fonctionner un modèle ML pour un cluster HDInsight Spark 1.6 ainsi que pour un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="e7462-109">Setup steps and the code to operationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="e7462-110">Le code de ces procédures est également fourni dans les notebooks Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e7462-110">The code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="e7462-111">Notebook pour Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="e7462-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="e7462-112">Le notebook Jupyter [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) montre comment utiliser un modèle enregistré à l’aide de Python sur des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7462-112">The [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how to operationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="e7462-113">Notebook pour Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="e7462-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="e7462-114">Pour modifier le notebook Jupyter pour Spark 1.6 afin de l’utiliser avec un cluster HDInsight Spark 2.0, remplacez le fichier de code Python par [ce fichier](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="e7462-114">To modify the Jupyter notebook for Spark 1.6 to use with an HDInsight Spark 2.0 cluster, replace the Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="e7462-115">Ce code montre comment utiliser les modèles créés dans Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="e7462-115">This code shows how to consume the models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e7462-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e7462-116">Prerequisites</span></span>

1. <span data-ttu-id="e7462-117">Vous avez besoin d’un compte Azure et d’un cluster HDInsight Spark 1.6 (ou Spark 2.0) pour effectuer cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="e7462-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="e7462-118">Pour obtenir des instructions sur la façon de satisfaire à ces exigences, voir [Vue d’ensemble de la science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7462-118">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="e7462-119">Cette rubrique contient également une description des données NYC 2013 Taxi utilisées ici, et des instructions sur l’exécution de code à partir d’un bloc-notes Jupyter sur le cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-119">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 
2. <span data-ttu-id="e7462-120">Vous devez également créer les modèles Machine Learning à noter ici en appliquant la procédure de la rubrique [Exploration et modélisation des données avec Spark](machine-learning-data-science-spark-data-exploration-modeling.md) pour le cluster Spark 1.6 ou les notebooks Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="e7462-120">You must also create the machine learning models to be scored here by working through the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for the Spark 1.6 cluster or the Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="e7462-121">Les notebooks Spark 2.0 utilisent un jeu de données supplémentaire pour la tâche de classification, le jeu de données bien connu sur les départs à l’heure des compagnies aériennes pour les années 2011 et 2012.</span><span class="sxs-lookup"><span data-stu-id="e7462-121">The Spark 2.0 notebooks use an additional data set for the classification task, the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="e7462-122">Une description des notebooks et des liens vers ceux-ci sont fournis dans le fichier [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) correspondant au dépôt GitHub qui les contient.</span><span class="sxs-lookup"><span data-stu-id="e7462-122">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="e7462-123">En outre, le code présenté ici et dans les notebooks liés est générique et doit fonctionner sur n’importe quel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-123">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="e7462-124">Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et de gestion de cluster peuvent être légèrement différentes de celles indiquées ici.</span><span class="sxs-lookup"><span data-stu-id="e7462-124">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="e7462-125">Configuration : emplacements de stockage, bibliothèques et contexte Spark prédéfini</span><span class="sxs-lookup"><span data-stu-id="e7462-125">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="e7462-126">Spark peut lire et écrire dans un objet blob Stockage Azure (également appelé WASB).</span><span class="sxs-lookup"><span data-stu-id="e7462-126">Spark is able to read and write to an Azure Storage Blob (WASB).</span></span> <span data-ttu-id="e7462-127">Donc, vos données stockées dedans sont exploitables par Spark et les résultats peuvent être stockés à nouveau dans WASB.</span><span class="sxs-lookup"><span data-stu-id="e7462-127">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="e7462-128">Pour enregistrer les modèles ou les fichiers dans WASB, le chemin d’accès doit être correctement spécifié.</span><span class="sxs-lookup"><span data-stu-id="e7462-128">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="e7462-129">Le conteneur par défaut associé au cluster Spark peut être référencé à l’aide d’un chemin commençant par *"wasb//"*.</span><span class="sxs-lookup"><span data-stu-id="e7462-129">The default container attached to the Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="e7462-130">L’exemple de code suivant spécifie l’emplacement des données à lire et le chemin d’accès au répertoire de stockage dans lequel la sortie du modèle est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="e7462-130">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="e7462-131">Définir les chemins d’accès aux emplacements de stockage dans WASB</span><span class="sxs-lookup"><span data-stu-id="e7462-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="e7462-132">Les modèles sont enregistrés dans : wasb:///user/remoteuser/NYCTaxi/Models.</span><span class="sxs-lookup"><span data-stu-id="e7462-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="e7462-133">Si ce chemin d’accès n’est pas défini correctement, les modèles ne sont pas chargés en vue de leur notation.</span><span class="sxs-lookup"><span data-stu-id="e7462-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="e7462-134">Les résultats notés sont enregistrés dans : wasb:///user/remoteuser/NYCTaxi/ScoredResults.</span><span class="sxs-lookup"><span data-stu-id="e7462-134">The scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="e7462-135">Si le chemin d’accès au dossier est incorrect, les résultats ne sont pas enregistrés dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="e7462-135">If the path to folder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="e7462-136">Les chemins des fichiers peuvent être copiés et collés dans les espaces réservés à cet effet dans le code à partir de la sortie de la dernière cellule du notebook **machine-learning-data-science-spark-data-exploration-modeling.ipynb** .</span><span class="sxs-lookup"><span data-stu-id="e7462-136">The file path locations can be copied and pasted into the placeholders in this code from the output of the last cell of the **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="e7462-137">Voici le code pour définir les chemins de répertoires :</span><span class="sxs-lookup"><span data-stu-id="e7462-137">Here is the code to set directory paths:</span></span> 

    # LOCATION OF DATA TO BE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR THE MODELS TO BE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="e7462-138">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-138">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="e7462-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="e7462-140">Importer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="e7462-140">Import libraries</span></span>
<span data-ttu-id="e7462-141">Définir le contexte Spark et importer les bibliothèques nécessaires avec le code suivant</span><span class="sxs-lookup"><span data-stu-id="e7462-141">Set spark context and import necessary libraries with the following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="e7462-142">Contexte Spark prédéfini et commandes magiques PySpark</span><span class="sxs-lookup"><span data-stu-id="e7462-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="e7462-143">Les noyaux PySpark fournis avec les blocs-notes Jupyter comprennent un contexte prédéfini.</span><span class="sxs-lookup"><span data-stu-id="e7462-143">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="e7462-144">Vous n’avez donc pas besoin de définir explicitement les contextes Spark ou Hive avant de commencer à utiliser l’application que vous développez.</span><span class="sxs-lookup"><span data-stu-id="e7462-144">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="e7462-145">Ils sont disponibles pour vous par défaut.</span><span class="sxs-lookup"><span data-stu-id="e7462-145">These are available for you by default.</span></span> <span data-ttu-id="e7462-146">Ces contextes sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="e7462-146">These contexts are:</span></span>

* <span data-ttu-id="e7462-147">sc : pour Spark</span><span class="sxs-lookup"><span data-stu-id="e7462-147">sc - for Spark</span></span> 
* <span data-ttu-id="e7462-148">sqlContext : pour Hive</span><span class="sxs-lookup"><span data-stu-id="e7462-148">sqlContext - for Hive</span></span>

<span data-ttu-id="e7462-149">Le noyau PySpark fournit certaines « commandes magiques » prédéfinies, qui sont des commandes spéciales que vous pouvez appeler avec %%.</span><span class="sxs-lookup"><span data-stu-id="e7462-149">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="e7462-150">Deux de ces commandes sont utilisées dans ces exemples de code.</span><span class="sxs-lookup"><span data-stu-id="e7462-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="e7462-151">**%%local** Indique que le code des lignes suivantes est exécuté localement.</span><span class="sxs-lookup"><span data-stu-id="e7462-151">**%%local** Specified that the code in subsequent lines is executed locally.</span></span> <span data-ttu-id="e7462-152">Le code doit être du code Python valide.</span><span class="sxs-lookup"><span data-stu-id="e7462-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="e7462-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="e7462-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="e7462-154">Exécute une requête Hive sur sqlContext.</span><span class="sxs-lookup"><span data-stu-id="e7462-154">Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="e7462-155">Si le paramètre -o est passé, le résultat de la requête est conservé dans le contexte Python %%local en tant que tableau de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="e7462-155">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="e7462-156">Pour plus d’informations sur les noyaux pour blocs-notes Jupyter et sur les « commandes magiques » qu’ils fournissent, voir [Noyaux disponibles pour les blocs-notes Jupyter avec les clusters HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="e7462-156">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="e7462-157">Recevoir les données et créer une trame de données nettoyée</span><span class="sxs-lookup"><span data-stu-id="e7462-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="e7462-158">Cette section contient le code d’une série de tâches nécessaires à la réception de l’échantillon de données à modéliser.</span><span class="sxs-lookup"><span data-stu-id="e7462-158">This section contains the code for a series of tasks required to ingest the data to be scored.</span></span> <span data-ttu-id="e7462-159">Lire un échantillon de 0,1 % du fichier contenant les trajets et prix de taxi (stocké dans un fichier TSV), formater les données et créer une trame de données propre.</span><span class="sxs-lookup"><span data-stu-id="e7462-159">Read in a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file), format the data, and then creates a clean data frame.</span></span>

<span data-ttu-id="e7462-160">Les fichiers de trajet et de prix de taxi ont été joints dans la procédure décrite dans la rubrique [Processus TDSP (Team Data Science Process) en action : Utilisation de clusters HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) .</span><span class="sxs-lookup"><span data-stu-id="e7462-160">The taxi trip and fare files were joined based on the procedure provided in the: [The Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e7462-161">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-161">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-162">Durée d’exécution de la cellule ci-dessus : 46,37 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-162">Time taken to execute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="e7462-163">Préparer les données à la notation dans Spark</span><span class="sxs-lookup"><span data-stu-id="e7462-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="e7462-164">Cette section montre comment indexer, encoder et mettre à l’échelle des caractéristiques catégorielles en vue de leur utilisation dans les algorithmes d’apprentissage contrôlé MLlib pour la classification et la régression.</span><span class="sxs-lookup"><span data-stu-id="e7462-164">This section shows how to index, encode, and scale categorical features to prepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="e7462-165">Transformation de caractéristiques : indexer et encoder des caractéristiques catégorielles en vue de leur utilisation dans des modèles à noter</span><span class="sxs-lookup"><span data-stu-id="e7462-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="e7462-166">Cette section montre comment indexer les données catégorielles à l’aide d’un `StringIndexer` et encoder les caractéristiques avec entrée de `OneHotEncoder` dans les modèles.</span><span class="sxs-lookup"><span data-stu-id="e7462-166">This section shows how to index categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into the models.</span></span>

<span data-ttu-id="e7462-167">[StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encode une colonne de libellés en une colonne d’index de libellés.</span><span class="sxs-lookup"><span data-stu-id="e7462-167">The [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels to a column of label indices.</span></span> <span data-ttu-id="e7462-168">Les index sont classés par fréquence de libellé.</span><span class="sxs-lookup"><span data-stu-id="e7462-168">The indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="e7462-169">[OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mappe une colonne d’index de libellés à une colonne de vecteurs binaires, contenant au plus une valeur 1.</span><span class="sxs-lookup"><span data-stu-id="e7462-169">The [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="e7462-170">Cet encodage autorise les algorithmes qui appliquent des caractéristiques numériques continues, comme la régression logistique, à des caractéristiques catégorielles.</span><span class="sxs-lookup"><span data-stu-id="e7462-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, to be applied to categorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is the cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e7462-171">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-171">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-172">Durée d’exécution de la cellule ci-dessus : 5,37 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-172">Time taken to execute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="e7462-173">Créer des objets RDD avec des tableaux de caractéristiques à intégrer dans des modèles</span><span class="sxs-lookup"><span data-stu-id="e7462-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="e7462-174">Cette section contient le code montrant comment indexer des données textuelles catégorielles en un objet RDD et les encoder linéairement pour qu’elles puissent former et tester la régression logistique de MLlib et d’autres modèles de classification.</span><span class="sxs-lookup"><span data-stu-id="e7462-174">This section contains code that shows how to index categorical text data as an RDD object and one-hot encode it so it can be used to train and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="e7462-175">Les données indexées sont stockées dans des objets [RDD (Resilient Distributed Dataset)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) .</span><span class="sxs-lookup"><span data-stu-id="e7462-175">The indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="e7462-176">Il s’agit de l’abstraction de base dans Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-176">These are the basic abstraction in Spark.</span></span> <span data-ttu-id="e7462-177">Un objet RDD représente une collection immuable et partitionnée d’éléments qui peuvent faire l’objet d’un traitement en parallèle avec Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="e7462-178">Il contient également du code montrant comment mettre à l’échelle des données avec le `StandardScalar` fourni par MLlib, en vue d’une utilisation dans la régression linéaire avec SGD (Stochastic Gradient Descent), un algorithme répandu permettant de former une large gamme de modèles Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e7462-178">It also contains code that shows how to scale data with the `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="e7462-179">[StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) permet de mettre à l’échelle les caractéristiques en fonction de la variance d’unité.</span><span class="sxs-lookup"><span data-stu-id="e7462-179">The [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used to scale the features to unit variance.</span></span> <span data-ttu-id="e7462-180">La mise à l’échelle des caractéristiques, également appelée normalisation des données, garantit que les caractéristiques aux valeurs très dispersées sont pondérées dans la fonction cible.</span><span class="sxs-lookup"><span data-stu-id="e7462-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e7462-181">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-181">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-182">Durée d’exécution de la cellule ci-dessus : 11,72 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-182">Time taken to execute above cell: 11.72 seconds</span></span>

## <a name="score-with-the-logistic-regression-model-and-save-output-to-blob"></a><span data-ttu-id="e7462-183">Noter avec le modèle de régression logistique et enregistrer la sortie dans l’objet BLOB</span><span class="sxs-lookup"><span data-stu-id="e7462-183">Score with the Logistic Regression Model and save output to blob</span></span>
<span data-ttu-id="e7462-184">Le code de cette section montre comment charger un modèle de régression logistique enregistré dans Azure Blob Storage et l’utiliser pour prédire si un pourboire est payé lors d’un trajet en taxi, le noter avec des mesures de classification standard, l’enregistrer puis représenter graphiquement les résultats dans Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e7462-184">The code in this section shows how to load a Logistic Regression Model that has been saved in Azure blob storage and use it to predict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot the results to blob storage.</span></span> <span data-ttu-id="e7462-185">Les résultats notés sont stockés dans des objets RDD.</span><span class="sxs-lookup"><span data-stu-id="e7462-185">The scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) TO BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="e7462-186">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-186">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-187">Durée d’exécution de la cellule ci-dessus : 19,22 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-187">Time taken to execute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="e7462-188">Noter un modèle de régression linéaire</span><span class="sxs-lookup"><span data-stu-id="e7462-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="e7462-189">Nous avons utilisé [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) pour former un modèle de régression linéaire utilisant SGD (Stochastic Gradient Descent) à des fins d’optimisation pour prédire le montant des pourboires payés.</span><span class="sxs-lookup"><span data-stu-id="e7462-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) to train a linear regression model using Stochastic Gradient Descent (SGD) for optimization to predict the amount of tip paid.</span></span> 

<span data-ttu-id="e7462-190">Le code de cette section montre comment charger un modèle de régression linéaire à partir d’Azure Blob Storage, le noter avec des variables mises à l’échelle, puis réenregistrer les résultats dans l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e7462-190">The code in this section shows how to load a Linear Regression Model from Azure blob storage, score using scaled variables, and then save the results back to the blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e7462-191">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-191">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-192">Durée d’exécution de la cellule ci-dessus : 16,63 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-192">Time taken to execute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="e7462-193">Noter les modèles Forêts aléatoires de classification et de régression</span><span class="sxs-lookup"><span data-stu-id="e7462-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="e7462-194">Le code de cette section montre comment charger les modèles Forêts aléatoires de classification et de régression enregistrés dans Azure Blob Storage, noter leurs performances avec des mesures standard de classificateur et de régression, puis réenregistrer les résultats dans Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e7462-194">The code in this section shows how to load the saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span>

<span data-ttu-id="e7462-195">[forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="e7462-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="e7462-196">Elles combinent de nombreux arbres de décision pour réduire le risque de surajustement.</span><span class="sxs-lookup"><span data-stu-id="e7462-196">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="e7462-197">Elles gèrent les caractéristiques catégorielles, prennent en compte le paramètre de classification multiclasse, ne requièrent aucune mise à l’échelle des caractéristiques et peuvent capturer les non-linéarités ainsi que les interactions entre les caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="e7462-197">Random forests can handle categorical features, extend to the multiclass classification setting, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="e7462-198">Les forêts aléatoires constituent l’un des modèles Machine Learning les plus performants pour la classification et la régression.</span><span class="sxs-lookup"><span data-stu-id="e7462-198">Random forests are one of the most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="e7462-199">[spark.mllib](http://spark.apache.org/mllib/) prend en charge les forêts aléatoires pour la classification binaire et multiclasse et pour la régression, à l’aide des caractéristiques continues et catégorielles.</span><span class="sxs-lookup"><span data-stu-id="e7462-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="e7462-200">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-200">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-201">Durée d’exécution de la cellule ci-dessus : 31,07 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-201">Time taken to execute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="e7462-202">Noter les modèles GBT de classification et de régression</span><span class="sxs-lookup"><span data-stu-id="e7462-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="e7462-203">Le code de cette section montre comment charger les modèles GBT de classification et de régression enregistrés dans Azure Blob Storage, noter leurs performances avec des mesures standard de classificateur et de régression, puis réenregistrer les résultats dans Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e7462-203">The code in this section shows how to load classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span> 

<span data-ttu-id="e7462-204">**spark.mllib** prend en charge les arbres GBT pour la classification binaire et la régression, à l’aide des caractéristiques continues et catégorielles.</span><span class="sxs-lookup"><span data-stu-id="e7462-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="e7462-205">[Gradient Boosted Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="e7462-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="e7462-206">Ils aident les arbres de décision à minimiser itérativement une fonction de perte.</span><span class="sxs-lookup"><span data-stu-id="e7462-206">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="e7462-207">Ils gèrent les caractéristiques catégorielles, ne requièrent aucune mise à l’échelle des caractéristiques et peuvent capturer les non-linéarités ainsi que les interactions entre les caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="e7462-207">GBTs can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="e7462-208">Ils s’utilisent également dans le paramétrage de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="e7462-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    #LOAD AND SCORE THE MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e7462-209">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-209">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-210">Durée d’exécution de la cellule ci-dessus : 14,6 secondes</span><span class="sxs-lookup"><span data-stu-id="e7462-210">Time taken to execute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="e7462-211">Nettoyer des objets de la mémoire et imprimer les emplacements de fichier notés</span><span class="sxs-lookup"><span data-stu-id="e7462-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH TO SCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="e7462-212">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="e7462-212">**OUTPUT:**</span></span>

<span data-ttu-id="e7462-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="e7462-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="e7462-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="e7462-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="e7462-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="e7462-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="e7462-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="e7462-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="e7462-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="e7462-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="e7462-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="e7462-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="e7462-219">Utiliser les modèles Spark via une interface web</span><span class="sxs-lookup"><span data-stu-id="e7462-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="e7462-220">Spark fournit un mécanisme permettant de soumettre à distance des travaux par lots ou des requêtes interactives via une interface REST dotée d’un composant appelé Livy.</span><span class="sxs-lookup"><span data-stu-id="e7462-220">Spark provides a mechanism to remotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="e7462-221">Par défaut, Livy est activé sur votre cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="e7462-222">Pour plus d’informations sur Livy, consultez [Envoi de travaux Spark à distance en utilisant Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="e7462-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="e7462-223">Vous pouvez utiliser Livy pour envoyer à distance un travail qui note un fichier stocké dans un objet blob Azure, puis consigne les résultats dans un autre objet blob.</span><span class="sxs-lookup"><span data-stu-id="e7462-223">You can use Livy to remotely submit a job that batch scores a file that is stored in an Azure blob and then writes the results to another blob.</span></span> <span data-ttu-id="e7462-224">Pour ce faire, téléchargez le script Python à partir de </span><span class="sxs-lookup"><span data-stu-id="e7462-224">To do this, you upload the Python script from</span></span>  
<span data-ttu-id="e7462-225">[Github](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) dans l’objet blob du cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) to the blob of the Spark cluster.</span></span> <span data-ttu-id="e7462-226">Vous pouvez utiliser un outil tel que l’**Explorateur de stockage Microsoft Azure** ou **AzCopy** pour copier le script dans l’objet blob de cluster.</span><span class="sxs-lookup"><span data-stu-id="e7462-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** to copy the script to the cluster blob.</span></span> <span data-ttu-id="e7462-227">Dans le cas présent, nous avons chargé le script ***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="e7462-227">In our case we uploaded the script to ***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="e7462-228">Les clés d’accès dont vous avez besoin se trouvent sur le portail du compte de stockage associé au cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-228">The access keys that you need can be found on the portal for the storage account associated with the Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="e7462-229">Une fois chargé à cet emplacement, ce script s’exécute au sein du cluster Spark dans un contexte distribué.</span><span class="sxs-lookup"><span data-stu-id="e7462-229">Once uploaded to this location, this script runs within the Spark cluster in a distributed context.</span></span> <span data-ttu-id="e7462-230">Il charge le modèle et exécute les prévisions sur les fichiers d’entrée en fonction du modèle.</span><span class="sxs-lookup"><span data-stu-id="e7462-230">It loads the model and runs predictions on input files based on the model.</span></span>  

<span data-ttu-id="e7462-231">Vous pouvez exécuter ce script à distance en effectuant une simple requête HTTPS/REST sur Livy.</span><span class="sxs-lookup"><span data-stu-id="e7462-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="e7462-232">Voici une commande curl permettant de créer la requête HTTP qui appelle le script Python à distance.</span><span class="sxs-lookup"><span data-stu-id="e7462-232">Here is a curl command to construct the HTTP request to invoke the Python script remotely.</span></span> <span data-ttu-id="e7462-233">Remplacez CLUSTERLOGIN, CLUSTERPASSWORD et CLUSTERNAME par les valeurs appropriées pour votre cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e7462-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with the appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND TO INVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="e7462-234">Vous pouvez utiliser n’importe quel langage sur le système distant pour appeler la tâche Spark via Livy, par un simple appel HTTPS avec l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="e7462-234">You can use any language on the remote system to invoke the Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="e7462-235">Il vaut mieux utiliser la bibliothèque de requêtes Python pour effectuer cet appel HTTP, mais elle n’est pas installée par défaut dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e7462-235">It would be convenient to use the Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="e7462-236">C’est pourquoi les anciennes bibliothèques HTTP sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="e7462-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="e7462-237">Voici le code Python pour l’appel HTTP :</span><span class="sxs-lookup"><span data-stu-id="e7462-237">Here is the Python code for the HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF THE REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY THE PYTHON SCRIPT TO RUN ON THE SPARK CLUSTER
    # IN THE FILE PARAMETER OF THE JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="e7462-238">Vous pouvez également ajouter ce code Python dans [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) pour soumettre un travail Spark qui évalue un objet blob en fonction de divers événements, comme un minuteur, une création ou la mise à jour d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="e7462-238">You can also add this Python code to [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) to trigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="e7462-239">Si vous préférez vous passer de code, utilisez [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) pour appeler la notation groupée Spark en définissant une action HTTP dans le **Concepteur d’applications logiques** et en définissant ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="e7462-239">If you prefer a code free client experience, use the [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) to invoke the Spark batch scoring by defining an HTTP action on the **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="e7462-240">Sur le portail Azure, créez une application logique en sélectionnant **+Nouveau** -> **Web + Mobile** -> **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="e7462-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="e7462-241">Pour afficher le **Concepteur d’applications logiques**, entrez le nom de l’application logique et le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e7462-241">To bring up the **Logic Apps Designer**, enter the name of the Logic App and App Service Plan.</span></span>
* <span data-ttu-id="e7462-242">Sélectionnez une action HTTP, puis entrez les paramètres indiqués dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="e7462-242">Select an HTTP action and enter the parameters shown in the following figure:</span></span>

![Concepteur Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="e7462-244">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="e7462-244">What's next?</span></span>
<span data-ttu-id="e7462-245">**Validation croisée et balayage hyperparamétrique**: consultez [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment effectuer la formation des modèles à l’aide de la validation croisée et du balayage hyperparamétrique.</span><span class="sxs-lookup"><span data-stu-id="e7462-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

