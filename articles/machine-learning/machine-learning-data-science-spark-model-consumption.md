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
# <a name="operationalize-spark-built-machine-learning-models"></a>Faire fonctionner les modèles Machine Learning créés avec Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Cette rubrique montre comment toooperationalize un modèle d’apprentissage ordinateur enregistré (ML) à l’aide de Python sur HDInsight Spark clusters. Il décrit comment les modèles d’apprentissage qui ont été générées à l’aide de Spark MLlib et stockées dans le stockage des objets Blob Azure (WASB) de l’ordinateur tooload et tooscore les jeux de données qui ont également été stockées dans WASB. Il montre comment toopre à traiter les données d’entrée de hello, à l’aide des fonctionnalités de transformation hello des fonctions d’indexation et l’encodage dans hello MLlib toolkit, et comment toocreate un objet de données étiqueté point qui peut être utilisé comme entrée pour calculer les scores des modèles de hello ML. les modèles de Hello utilisés pour calculer les scores incluent la régression linéaire, régression logistique, les modèles de forêt aléatoire et modèles d’arbre de Gradient Boosting.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Clusters Spark et notebooks Jupyter
Étapes de configuration et toooperationalize de code hello un modèle ML sont fournies dans cette procédure pas à pas pour l’utilisation d’un cluster HDInsight Spark 1.6 ainsi que d’un cluster Spark 2.0. code Hello de ces procédures est également fourni dans les blocs-notes Notebook.

### <a name="notebook-for-spark-16"></a>Notebook pour Spark 1.6
Hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) bloc-notes jupyter montre comment toooperationalize un modèle enregistré à l’aide de Python sur HDInsight clusters. 

### <a name="notebook-for-spark-20"></a>Notebook pour Spark 2.0
toomodify hello notebook ordinateur portable pour toouse Spark 1.6 avec un cluster HDInsight Spark 2.0, remplacez le fichier de code Python hello avec [ce fichier](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Ce code montre comment les modèles de hello tooconsume créés dans Spark 2.0.


## <a name="prerequisites"></a>Composants requis

1. Vous avez besoin d’un compte Azure et un Spark 1.6 (ou Spark 2.0) du cluster HDInsight toocomplete cette procédure pas à pas. Consultez hello [vue d’ensemble de science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md) pour obtenir des instructions sur la façon de toosatisfy ces exigences. Cette rubrique contient également une description de type hello données NYC 2013 Taxi utilisées ici et obtenir des instructions sur la façon dont tooexecute code à partir d’un bloc-notes jupyter sur cluster Spark de hello. 
2. Vous devez également créer hello modèles d’apprentissage automatique toobe notées ici en passant par hello [exploration de données et modélisation avec Spark](machine-learning-data-science-spark-data-exploration-modeling.md) rubrique pour le cluster de hello Spark 1.6 ou les blocs-notes hello Spark 2.0. 
3. les blocs-notes Hello Spark 2.0 utilisent un jeu de données supplémentaire pour tâche de classification hello, hello connu compagnie aérienne à temps départ dataset à partir de 2011 et 2012. Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent. En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark. Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Le programme d’installation : hello, les bibliothèques et les emplacements de stockage prédéfinir le contexte de Spark
Spark est en mesure de tooan de tooread et écriture objet Blob de stockage Azure (WASB). Par conséquent, vos données existantes qui y sont stockées peuvent être traitées à l’aide de Spark et hello stockées dans WASB des résultats.

toosave modèles ou les fichiers dans WASB, chemin d’accès hello doit toobe correctement spécifiée. Hello du cluster Spark toohello conteneur attaché par défaut peut être référencé à l’aide d’un chemin commençant par : *« wasb / / »*. exemple de code suivant Hello spécifie emplacement hello de hello toobe de données en lecture et chemin d’accès de hello pour hello modèle stockage toowhich hello modèle de sortie est enregistré. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Définir les chemins d’accès aux emplacements de stockage dans WASB
Les modèles sont enregistrés dans : wasb:///user/remoteuser/NYCTaxi/Models. Si ce chemin d’accès n’est pas défini correctement, les modèles ne sont pas chargés en vue de leur notation.

Hello score résultats ont été enregistrés dans : « wasb : / / / utilisateur/UtilisateurDistant/NYCTaxi/ScoredResults ». Si toofolder de chemin d’accès hello est incorrecte, les résultats ne sont pas enregistrés dans le dossier.   

> [!NOTE]
> emplacements de chemin d’accès de fichier Hello peuvent être copiés et collés dans des espaces réservés de hello dans ce code de sortie de hello de hello dernière cellule de hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** bloc-notes.   
> 
> 

Voici les chemins d’accès du répertoire tooset code hello : 

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

**SORTIE :**

datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Importer les bibliothèques
Définir le contexte de spark et importer des bibliothèques nécessaires avec hello suivant de code

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


### <a name="preset-spark-context-and-pyspark-magics"></a>Contexte Spark prédéfini et commandes magiques PySpark
noyaux PySpark Hello qui sont fournis avec les ordinateurs portables Notebook ont un contexte prédéfini. Par conséquent, il est inutile tooset hello Spark ou ruche contextes explicitement avant de commencer à utiliser avec l’application hello que vous développez. Ils sont disponibles pour vous par défaut. Ces contextes sont les suivants :

* sc : pour Spark 
* sqlContext : pour Hive

Hello PySpark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec %%. Deux de ces commandes sont utilisées dans ces exemples de code.

* **%% local** spécifié que le code hello dans les lignes suivantes est exécuté localement. Le code doit être du code Python valide.
* **%%sql -o <variable name>** 
* Exécute une requête Hive sur hello sqlContext. Si le paramètre -o de hello est transmis, résultat hello de requête de hello est conservé dans hello %% contexte Python local en tant qu’une trame de données Pandas.

Pour plus d’informations sur les noyaux hello pour notebook blocs-notes et hello prédéfinies « magics » qui elles fournissent, consultez [clusters de noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Recevoir les données et créer une trame de données nettoyée
Cette section contient le code hello pour une série de tâches requise tooingest hello données toobe transformée. Lire dans un exemple de 0,1 % jointes de hello taxi voyage et tarif de fichier (stocké sous la forme d’un fichier .tsv), des données au format hello et crée ensuite une trame de données propre.

Hello taxi voyage et tarif les fichiers ont été joints en fonction de procédure hello fourni dans le : [hello du processus de science des données équipe en action : à l’aide de clusters HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) rubrique.

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 46.37 secondes

## <a name="prepare-data-for-scoring-in-spark"></a>Préparer les données à la notation dans Spark
Cette section montre comment tooindex, coder et mettre à l’échelle tooprepare fonctionnalités catégorielles pour utilisent dans les algorithmes d’apprentissage automatique de MLlib contrôlé pour la classification et de régression.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Transformation de caractéristiques : indexer et encoder des caractéristiques catégorielles en vue de leur utilisation dans des modèles à noter
Cette section montre comment à l’aide des données catégorielles tooindex un `StringIndexer` et coder les fonctionnalités avec `OneHotEncoder` d’entrée dans les modèles hello.

Hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encode une colonne de chaîne de la colonne d’étiquettes de tooa d’index de l’étiquette. indices de Hello sont classés par fréquence d’étiquette. 

Hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mappe une colonne de la colonne de tooa étiquette indices de vecteurs binaire, au maximum une seule une valeur. Cet encodage permet d’algorithmes qui attendent des fonctionnalités à valeurs continues, telles que la régression logistique, fonctionnalités de toocategorical toobe appliqué.

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 5.37 secondes

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Créer des objets RDD avec des tableaux de caractéristiques à intégrer dans des modèles
Cette section contient le code qui montre comment les données de texte catégorielles tooindex comme un RDD de l’objet et à chaud de celui Encoder donc il peut être utilisé tootrain et test MLlib régression logistique et les modèles basés sur l’arborescence. les données indexées Hello sont stockées dans [résilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objets. Il s’agit d’abstraction de base hello dans Spark. Un objet RDD représente une collection immuable et partitionnée d’éléments qui peuvent faire l’objet d’un traitement en parallèle avec Spark.

Il contient également le code qui montre comment les données tooscale avec hello `StandardScalar` fournie par MLlib pour une utilisation dans la régression linéaire avec stochastique dégradé descente (SGD), un algorithme populaire pour l’apprentissage d’un large éventail de modèles d’apprentissage automatique. Hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale utilisé hello fonctionnalités toounit écart. Fonctionnalité mise à l’échelle, également appelé normalisation des données, ainsi que des fonctionnalités avec des valeurs largement dispersées sont pas donné excessive peser en fonction de l’objectif hello. 

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 11.72 secondes

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Score avec hello modèle de régression logistique et enregistrer la sortie tooblob
code Hello dans cette section explique comment tooload un modèle de régression logistique qui a été enregistré dans Azure stockage d’objets blob et utiliser toopredict ou non une info-bulle est payée sur un voyage taxi, il score avec les mesures de classification standard et puis enregistrez et tracer hello résultats tooblob stockage. Hello résultats évalué sont stockées dans les objets RDD. 

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 19.22 secondes

## <a name="score-a-linear-regression-model"></a>Noter un modèle de régression linéaire
Nous avons utilisé [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) payé de tootrain un modèle de régression linéaire à l’aide de descente de Gradient stochastique (SGD) toopredict hello pendant l’optimisation d’info-bulle. 

code Hello dans cette section explique comment les tooload un modèle de régression linéaire à partir du stockage d’objets blob Azure, score à l’aide de variables à l’échelle et puis enregistrez les objets blob de hello résultats toohello précédent.

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


**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 16.63 secondes

## <a name="score-classification-and-regression-random-forest-models"></a>Noter les modèles Forêts aléatoires de classification et de régression
code Hello dans cette section montre comment les hello tooload enregistrées classification et les modèles forêt aléatoire de régression, enregistré dans le stockage d’objets blob Azure, un score de leurs performances avec classifieur standard et les mesures de régression, puis enregistrez hello résultats précédent tooblob stockage.

[forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.  Combiner des nombreux decision trees tooreduce hello des risques de dépassement de. Forêts aléatoires peuvent gérer les fonctionnalités catégorielles, étendre les paramètre de classification multiclasse toohello, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité. Forêts aléatoires sont un des hello plus de succès d’apprentissage des modèles pour la classification et la régression.

[spark.mllib](http://spark.apache.org/mllib/) prend en charge les forêts aléatoires pour la classification binaire et multiclasse et pour la régression, à l’aide des caractéristiques continues et catégorielles. 

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 31.07 secondes

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Noter les modèles GBT de classification et de régression
code Hello dans cette section montre comment classification de tooload et de régression des modèles d’arbre de Gradient Boosting à partir du stockage d’objets blob Azure, un score de leurs performances avec classifieur standard et les mesures de régression, puis enregistrez hello résultats précédent tooblob stockage. 

**spark.mllib** prend en charge les arbres GBT pour la classification binaire et la régression, à l’aide des caractéristiques continues et catégorielles. 

[Gradient Boosted Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision. Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte. GBTs peut gérer les fonctionnalités catégorielles, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité. Ils s’utilisent également dans le paramétrage de classification multiclasse.

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 14.6 secondes

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Nettoyer des objets de la mémoire et imprimer les emplacements de fichier notés
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


**SORTIE :**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Utiliser les modèles Spark via une interface web
Spark fournit un mécanisme tooremotely submit traitements ou requêtes interactives via un reste de l’interface avec un composant appelé Livy. Par défaut, Livy est activé sur votre cluster HDInsight Spark. Pour plus d’informations sur Livy, consultez [Envoi de travaux Spark à distance en utilisant Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

Vous pouvez utiliser Livy tooremotely soumettre un travail qui par lots scores un fichier qui est stocké dans un objet blob Azure, puis écrit blob de tooanother résultats hello. toodo, vous téléchargez le script Python hello  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) blob toohello de cluster de Spark hello. Vous pouvez utiliser un outil tel que **Microsoft Azure Storage Explorer** ou **AzCopy** le blob cluster toohello toocopy hello script. Dans notre cas, nous avons téléchargé script de hello trop***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Bonjour les touches d’accès rapide qui vous avez besoin se trouvent sur le portail de compte de stockage hello associé hello Spark cluster hello. 
> 
> 

Une fois téléchargé toothis emplacement, ce script s’exécute dans un cluster Spark de hello dans un contexte distribué. Il charge le modèle de hello et exécute des prédictions sur les fichiers d’entrée en fonction de modèle de hello.  

Vous pouvez exécuter ce script à distance en effectuant une simple requête HTTPS/REST sur Livy.  Voici un curl commande tooconstruct hello HTTP demande tooinvoke hello script Python à distance. Remplacez les valeurs appropriées hello pour votre cluster Spark CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

Vous pouvez utiliser n’importe quel langage sur hello distant tooinvoke hello Spark tâche système via Livy en effectuant un simple appel HTTPS avec l’authentification de base.   

> [!NOTE]
> Il serait bibliothèque de demandes de Python hello toouse pratique lors de l’établissement de cet appel HTTP, mais il n’est pas installé par défaut dans les fonctions d’Azure. C’est pourquoi les anciennes bibliothèques HTTP sont utilisées.   
> 
> 

Voici le code Python de hello pour l’appel de hello HTTP :

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


Vous pouvez également ajouter ce code Python trop[Azure fonctions](https://azure.microsoft.com/documentation/services/functions/) tootrigger une soumission de travaux Spark qui évalue un objet blob en fonction de divers événements comme un minuteur, la création ou la mise à jour d’un objet blob. 

Si vous préférez une expérience client libre de code, utilisez hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark score par lot en définissant une action HTTP sur hello **Concepteur d’applications logique** et en définissant ses paramètres. 

* Sur le portail Azure, créez une application logique en sélectionnant **+Nouveau** -> **Web + Mobile** -> **Application logique**. 
* toobring des hello **Concepteur d’applications logique**, entrez le nom hello hello logique d’application et le Plan App Service.
* Sélectionnez une action HTTP et entrez des paramètres de hello illustrés hello figure suivante :

![Concepteur Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Et ensuite ?
**Validation croisée et balayage hyperparamétrique**: consultez [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment effectuer la formation des modèles à l’aide de la validation croisée et du balayage hyperparamétrique.

