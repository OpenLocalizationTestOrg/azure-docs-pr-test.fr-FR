---
title: "aaaAdvanced l’exploration de données et de modélisation avec Spark | Documents Microsoft"
description: "Utiliser l’exploration de données toodo HDInsight Spark et l’apprentissage des modèles de classification et de régression binaire à l’aide de l’optimisation de la validation croisée et hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Modélisation et exploration avancées des données avec Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Cette procédure pas à pas utilise HDInsight Spark toodo exploration et train binaire classification des données et les modèles de régression à l’aide de la validation croisée et optimisation hyperparameter sur un échantillon de hello NYC taxi voyage serrées 2013 le jeu de données. Il vous guide à travers les étapes de hello Hello [processus de science des données](http://aka.ms/datascienceprocess), de bout en bout, à l’aide d’un HDInsight Spark cluster pour le traitement et les modèles de données et hello hello toostore d’objets BLOB Azure. processus de Hello explore et visualise les données importées à partir d’un objet Blob de stockage Azure et prépare ensuite les modèles prédictifs hello données toobuild. Python a été utilisé toocode hello solution et tooshow hello applique les tracés. Ces modèles sont build à l’aide de la classification binaire du toodo toolkit Spark MLlib hello et tâches de modélisation de régression. 

* Hello **classification binaire** tâche est toopredict ou non une info-bulle est payée pour le voyage de hello. 
* Hello **régression** tâche est toopredict hello Conseil hello basé sur d’autres fonctionnalités de l’info-bulle. 

étapes de modélisation Hello également contient de code montrant comment tootrain, évaluer et enregistrer chaque type de modèle. Hello rubrique traite des hello même sol comme hello [exploration de données et modélisation avec Spark](machine-learning-data-science-spark-data-exploration-modeling.md) rubrique. Mais il est plus « avancé » car elle utilise également la validation croisée avec hyperparameter balayage tootrain des modèles de classification et de régression précis de façon optimale. 

**La validation croisée (VC)** est une technique qui évalue la manière dont un modèle formé sur un jeu connu de données généralise toopredicting les fonctionnalités de hello des jeux de données sur lequel il n’a pas été effectué.  Une implémentation commune utilisée ici est toodivide un dataset en K plis, puis exécutez modèle hello de façon alternée sur tous les mais l’un des plis de hello. possibilité de Hello de hello modèle tooprediction précisément lorsque testé avec le jeu de données indépendant hello dans ce modèle de hello tootrain pli ne pas utilisé est évaluée.

**Optimisation de Hyperparameter** problème hello de choisir un ensemble d’hyperparamètres pour un algorithme d’apprentissage, généralement avec comme objectif hello d’optimisation d’une mesure des performances de l’algorithme hello sur un jeu de données indépendant. **Hyperparamètres** sont des valeurs qui doivent être spécifiés en dehors de la procédure de formation de modèle hello. Hypothèses sur ces valeurs peuvent avoir un impact sur une grande souplesse hello et la précision des modèles de hello. Les arbres de décision ont hyperparamètres, par exemple, telles que hello souhaité profondeur et nombre de feuilles dans l’arborescence de hello. Les machines à vecteurs de support nécessitent la configuration d’un terme de pénalité en cas d’erreur de classification. 

Une optimisation de hyperparameter de tooperform moyen couramment utilisée ici est une recherche de la grille, ou un **balayage de paramètre**. Il s’agit d’effectuer une recherche exhaustive des valeurs de hello un sous-ensemble spécifié de l’espace de hyperparameter hello pour un algorithme d’apprentissage. Validation croisée peut fournir un toosort de métriques de performances out produits par l’algorithme de recherche hello grille des résultats optimaux hello. CV utilisé avec hyperparameter de balayage des problèmes de limite permet le surajustement un tootraining de données de modèle, afin que le modèle hello conserve hello capacité tooapply toohello général jeu de données à partir de quels hello les données d’apprentissage ont été extraites.

Hello modèles que nous utilisons : régression logistique et linéaire, les forêts aléatoires et les arbres augmentés dégradés

* [La régression linéaire avec SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) est un modèle de régression linéaire qui utilise une méthode de descente Gradient stochastique (SGD) et pour l’optimisation et la fonctionnalité de mise à l’échelle des montants de conseil toopredict hello payé. 
* [La régression logistique avec LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou la régression « logit », est un modèle de régression qui peut être utilisé lors de la variable dépendante de hello est la classification des données catégorielles toodo. LBFGS est un algorithme d’optimisation quasi Newton qui rapproche algorithme Broyden – Fletcher – Goldfarb – Shanno (BFGS) de hello à l’aide d’une quantité limitée de mémoire de l’ordinateur, qui est largement utilisé dans l’apprentissage.
* [forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.  Combiner des nombreux decision trees tooreduce hello des risques de dépassement de. Forêts aléatoires sont utilisés pour la classification et de régression et peuvent gérer les fonctionnalités catégorielles et peuvent être étendus de paramètre de classification multiclasse toohello. Ils ne nécessitent pas la fonctionnalité mise à l’échelle et sont en mesure de toocapture non linéarité et interactions de fonctionnalité. Forêts aléatoires sont un des hello plus de succès d’apprentissage des modèles pour la classification et la régression.
* [Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision. Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte. GBTs sont utilisés pour la classification et de régression et peut gérer les fonctionnalités catégorielles, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité. Ils s’utilisent également dans le paramétrage de classification multiclasse.

Modélisation des exemples d’utilisation de CV et Hyperparameter balayage sont affichés pour le problème de classification binaire hello. Des exemples plus simples (sans paramètre balayages) sont présentés dans le sujet principal de hello pour les tâches de régression. Mais, dans l’annexe hello, validation à l’aide de net élastique pour régression linéaire et CV avec balayage de paramètre à l’aide de régression de forêt aléatoire est également présentée. Hello **élastique net** est une méthode de régression régularisée pour ajuster la droite de régression linéaire qui modélise linéairement combine les métriques L1 et L2 hello comme des sanctions Hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) et [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) méthodes.   

> [!NOTE]
> Bien que hello Spark MLlib toolkit est conçu toowork sur les jeux de données volumineux, un exemple relativement faible (à l’aide de K 170 lignes, environ 0,1 % du jeu de données hello d’origine NYC en ~ 30 Mo) est utilisé ici pour des raisons pratiques. exercice Hello donné ici s’exécute efficacement (en environ 10 minutes) sur un cluster HDInsight avec 2 nœuds de travail. Hello même code avec des modifications mineures, peut être utilisé tooprocess-jeux de données volumineux, avec les changements appropriés pour la mise en cache des données en mémoire et la modification de la taille de cluster hello.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Configuration : clusters et notebooks Spark
Les étapes de configuration et le code fournis dans cette procédure pas à pas concernent HDInsight Spark 1.6. Mais des notebooks Jupyter sont fournis pour les clusters HDInsight Spark 1.6 et Spark 2.0. Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent. En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark. Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici. Pour des raisons pratiques, voici les ordinateurs portables hello liens toohello Notebook pour Spark 1.6 et toobe 2.0 s’exécutent dans le noyau de pyspark hello Hello server de bloc-notes Jupyter :

### <a name="spark-16-notebooks"></a>Notebooks Spark 1.6

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) : inclut les thèmes du notebook 1 et traite également du développement de modèles à l’aide de l’ajustement des hyperparamètres et de la validation croisée.

### <a name="spark-20-notebooks"></a>Notebooks Spark 2.0

[Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ce fichier fournit des informations sur comment tooperform l’exploration de données, de modélisation et de calcul de score dans Spark 2.0 des clusters.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Le programme d’installation : hello, les bibliothèques et les emplacements de stockage prédéfinir le contexte de Spark
Spark est en mesure de tooAzure de tooread et écriture objet Blob de stockage (également appelé WASB). Par conséquent, vos données existantes qui y sont stockées peuvent être traitées à l’aide de Spark et hello stockées dans WASB des résultats.

toosave modèles ou les fichiers dans WASB, chemin d’accès hello doit toobe correctement spécifiée. Hello du cluster Spark toohello conteneur attaché par défaut peut être référencé à l’aide d’un chemin commençant par : « wasb : / / ». Les autres emplacements sont référencés par wasb://.

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Définir les chemins d’accès aux emplacements de stockage dans WASB
exemple de code suivant Hello spécifie emplacement hello de hello toobe de données en lecture et chemin d’accès de hello pour hello modèle stockage toowhich hello modèle de sortie est enregistré :

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**SORTIE**

datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Importer les bibliothèques
Importer des bibliothèques nécessaires avec hello suivant de code :

    # LOAD PYSPARK LIBRARIES
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
noyaux PySpark Hello qui sont fournis avec les ordinateurs portables Notebook ont un contexte prédéfini. Par conséquent, il est inutile tooset hello Spark ou ruche contextes explicitement avant de commencer à utiliser avec l’application hello que vous développez. Ces contextes sont disponibles pour vous par défaut. Ces contextes sont les suivants :

* sc : pour Spark 
* sqlContext : pour Hive

Hello PySpark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec %%. Deux de ces commandes sont utilisées dans ces exemples de code.

* **%% local** Spécifie que le code hello dans les lignes suivantes est toobe exécutée localement. Le code doit être du code Python valide.
* **%% -o sql <variable name>**  exécute une requête Hive sur hello sqlContext. Si le paramètre -o de hello est transmis, résultat hello de requête de hello est conservé dans hello %% contexte Python local en tant qu’une trame de données Pandas.

Pour plus d’informations sur les noyaux hello pour notebook blocs-notes et hello prédéfinies « magics » qui elles fournissent, consultez [clusters de noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Ingestion de données à partir d’un objet blob public :
Bonjour première étape dans le processus de science des données hello est tooingest hello données toobe analysée à partir de sources de son emplacement dans votre environnement de modélisation et exploration de données. Dans cette procédure, cet environnement est Spark. Cette section contient des toocomplete de code hello une série de tâches :

* réception hello données exemple toobe modélisée
* lire dans le jeu de données d’entrée hello (stockée sous la forme d’un fichier .tsv)
* format et hello nettoyer les données
* créer et mettre en cache des objets (RDD ou trames de données) en mémoire
* enregistrer les données en tant que table temporaire dans le contexte SQL.

Voici le code hello pour l’ingestion de données.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
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

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 276.62 secondes

## <a name="data-exploration--visualization"></a>Exploration et visualisation de données
Une fois les données de salutation a été placées dans Spark, hello étape suivante dans le processus de science des données hello est toogain une meilleure compréhension des données hello via l’exploration et visualisation. Dans cette section, nous examiner les données de taxi hello à l’aide de requêtes SQL et des variables de traçage hello cibles et des fonctionnalités potentiels pour l’examen visuel. Plus précisément, nous tracer fréquence hello passagers des nombres de dans taxi allers-retours, hello fréquence de quantités d’info-bulle, et comment les conseils varient selon le type et le montant du paiement.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Tracer un histogramme de fréquences d’inventaire passagers dans l’exemple hello de déplacements de taxi
Ce code et les extraits de code suivants utilisent SQL tooquery magique hello, exemple et les données de hello de tooplot magique local.

* **Magique SQL (`%%sql`)** hello HDInsight PySpark noyau prend en charge easy inline HiveQL requêtes contre hello sqlContext. Hello (-o nom_variable) argument persiste sortie hello de la requête SQL hello en tant qu’une trame de données Pandas sur le serveur de Notebook hello. Cela signifie qu’il est disponible en mode local de hello.
* Hello  **`%%local` magique** est toorun du code utilisé localement sur le serveur hello Notebook, qui est le nœud principal de hello du cluster HDInsight de hello. En général, vous utilisez `%%local` magique après hello `%%sql -o` magique est toorun utilisé une requête. paramètre de Hello -o soit persistant sortie hello de requête SQL hello localement. Puis hello `%%local` déclencheurs magiques hello ensemble suivant de toorun d’extraits de code localement par rapport à la sortie de hello de requêtes SQL hello qui a été rendu persistant localement. Hello sortie est automatiquement affichée après l’exécution de code de hello.

Cette requête extrait les allers-retours hello par nombre de passagers. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Ce code crée une trame de données locale à partir de la sortie de la requête hello et trace les données de salutation. Hello `%%local` magique crée une trame de données locale, `sqlResults`, qui peut être utilisé pour le traçage avec matplotlib. 

> [!NOTE]
> Cette commande magique PySpark est utilisée plusieurs fois lors de cette procédure pas à pas. Si la quantité de hello de données est importante, vous devez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Voici allers-retours de hello hello code tooplot par passager nombres

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**SORTIE**

![Fréquence des voyages par nombre de passagers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

Vous pouvez sélectionner parmi les différents types de visualisations (Table, à secteurs, ligne, zone ou barre) à l’aide de hello **Type** des boutons de menu dans le bloc-notes de hello. traçage de barre Hello est indiqué ici.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Tracez un histogramme du montant des pourboires et montrez comment le montant du pourboire varie selon le nombre de passagers et le montant des trajets.
Utiliser les données de toosample de requête SQL...

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


Cette cellule de code utilise hello SQL interroger toocreate trois graphiques hello des données.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**SORTIE :** 

![Distribution des montants de pourboire](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Conception des caractéristiques, transformation et préparation des données à modéliser
Cette section décrit et fournit le code hello pour les procédures utilisées tooprepare données pour une utilisation dans la modélisation de ML. Il montre des tâches de hello toodo suivant :

* Créer une caractéristique en partitionnant les heures dans des périodes de trafic
* Indexer et encoder des fonctionnalités catégorielles
* Créer des objets point étiquetés à intégrer dans les fonctions ML
* Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test
* Mise à l’échelle des caractéristiques
* Mettre en cache des objets en mémoire

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Créer une caractéristique en partitionnant les périodes de trafic dans les emplacements
Ce code montre comment toocreate une nouvelle fonctionnalité en partitionnant le trafic arrive dans emplacements, puis comment toocache hello résultant trame de données en mémoire. Mise en cache entraîne des temps d’exécution tooimproved où résilient Distributed jeux de données (RDDs) et les trames de données sont utilisés à plusieurs reprises. Par conséquent, nous mettons en cache les RDD et les trames de données à plusieurs stades de la procédure.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**SORTIE**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Indexer et encoder « à chaud » des fonctionnalités catégorielles
Cette section montre comment tooindex ou coder des fonctionnalités par catégorie pour l’entrée en hello modélisation des fonctions. Hello de modélisation et de prédire les fonctions de MLlib requièrent que les fonctionnalités avec les données d’entrée par catégorie être indexées ou encodées toouse préalable. 

Selon le modèle de hello, vous avez besoin de tooindex ou les codez de différentes façons. Par exemple, modèles logistique et de régression linéaire nécessitent à chaud un encodage, où, par exemple, une fonctionnalité avec trois catégories peut être développée dans les trois colonnes de fonctionnalités, avec chaque conteneur 0 ou 1 selon la catégorie hello d’une observation. Fournit des MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo à chaud un encodage de la fonction. Cet encodeur est mappé à une colonne de la colonne de tooa étiquette indices de vecteurs binaire, au maximum une seule une valeur. Cet encodage permet d’algorithmes qui attendent des fonctionnalités de valeurs numériques, telles que la régression logistique, fonctionnalités de toocategorical toobe appliqué.

Voici hello code tooindex et coder les fonctionnalités par catégorie :

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
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

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 3.14 secondes

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Créer des objets point étiquetés à intégrer dans les fonctions ML
Cette section contient le code qui montre comment le type de données de texte catégorielles tooindex sous forme de données étiqueté point et tooencode il. Il prépare régression logistique MLlib toobe utilisé tootrain et de test et autres modèles de classification. Les objets point étiquetés sont des jeux de données distribués résilients (RDD) mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes ML dans MLlib. Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.

Voici hello tooindex de code et de coder des fonctionnalités de texte pour la classification binaire.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Voici les fonctionnalités catégorielles texte tooencode et d’index pour l’analyse de régression linéaire de code hello.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test
Ce code crée un échantillonnage aléatoire de données hello (25 % est utilisé ici). Bien qu’il n’est pas requis pour cet exemple en raison de la taille de toohello du jeu de données hello, nous allons montrer comment vous pouvez échantillonner des données hello ici. Vous savez comment toouse pour votre propre problème si nécessaire. Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles. Ensuite, nous fractionner les exemple hello en une partie de la formation (75 % ici) et un test toouse de partie (25 % ici) dans la classification et la modélisation de régression.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 0,31 secondes

### <a name="feature-scaling"></a>Mise à l’échelle des caractéristiques
Fonctionnalité mise à l’échelle, également appelé normalisation des données, ainsi que des fonctionnalités avec des valeurs largement dispersées sont pas donné excessive peser en fonction de l’objectif hello. code de mise à l’échelle d’une fonctionnalité Hello utilise hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variance de toounit fonctionnalités tooscale hello. MLlib le fournit en vue d’une utilisation dans une régression linéaire avec SGD (Stochastic Gradient Descent). SGD est un algorithme populaire permettant de former une large gamme d’autres modèles Machine Learning, tels que les régressions régularisées ou les machines à vecteurs de support (SVM).   

> [!TIP]
> Nous avons trouvé hello LinearRegressionWithSGD algorithme toobe toofeature sensibles mise à l’échelle.   
> 
> 

Voici les variables de tooscale code hello pour une utilisation avec l’algorithme SGD hello régularisée linéaire.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 11.67 secondes

### <a name="cache-objects-in-memory"></a>Mettre en cache des objets en mémoire
Hello durée d’apprentissage et de test des algorithmes de ML peut être réduite par la trame de données d’entrée de hello objets utilisés pour la classification, la régression et, à l’échelle des fonctionnalités de mise en cache.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE** 

Temps nécessaire tooexecute au-dessus de la cellule : 0,13 secondes

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Prédire si un pourboire a été payé avec des modèles de classification binaires
Cette section montre comment utiliser trois modèles pour la tâche de classification binaire hello de prédiction ou non une info-bulle est payée pour un voyage taxi. les modèles Hello présentées sont :

* Régression logique 
* Forêts aléatoires
* Arbres GBT (Gradient Boosting Tree)

Chaque section de code générateur de modèle est divisée en étapes : 

1. **formation du modèle** avec un jeu de paramètres
2. **Évaluation de modèle** sur un jeu de données de test avec mesures
3. **Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure

Nous allons montrer comment toodo la validation croisée (VC) avec le paramètre de balayage de deux manières :

1. À l’aide de **générique** code personnalisé qui peut être l’algorithme tooany appliqué dans le paramètre MLlib et tooany définit dans l’algorithme. 
2. À l’aide de hello **pySpark fonction de pipeline CrossValidator**. Notez que CrossValidator présente quelques limitations pour Spark 1.5.0 : 
   
   * Les modèles de pipeline ne peuvent pas être enregistrés/conservés pour une consommation future.
   * Ne peut pas être utilisé pour chaque paramètre dans un modèle.
   * Ne peut pas être utilisé pour chaque algorithme MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Générique Cross-validation et balayage hyperparameter utilisés avec l’algorithme de régression logistique hello pour la classification binaire
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) qui prédit ou non une info-bulle est payée pour un voyage dans le jeu de données hello NYC taxi voyage et tarif. apprentissage du modèle Hello entre la validation (CV) et de balayage hyperparameter implémentée avec du code personnalisé qui peut être appliqué tooany Hello algorithmes dans MLlib d’apprentissage.   

> [!NOTE]
> l’exécution de Hello de ce code CV personnalisé peut prendre plusieurs minutes.
> 
> 

**L’apprentissage du modèle de régression logistique hello à l’aide de CV et hyperparameter balayage**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

Coefficients : [0,0082065285375, -0,0223675576104, -0,0183812028036, -3.48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]

Interception : -0,0111216486893

Temps nécessaire tooexecute au-dessus de la cellule : 14.43 secondes

**Évaluation du modèle de classification binaire hello avec métriques standard**

code Hello dans cette section montre comment tooevaluate une régression logistique modèle par rapport à un test-jeu de données, y compris un tracé de hello en courbe ROC.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

Zone sous PR = 0,985336538462

Zone sous ROC = 0,983383274312

Résumé des statistiques

Précision = 0,984174341679

Rappel = 0,984174341679

Score F1 = 0,984174341679

Temps nécessaire tooexecute au-dessus de la cellule : fréquence de 2,67 secondes

**Tracer la courbe ROC hello.**

Hello *predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente hello. *tmp_results* peuvent être utilisés toodo requêtes et produit des résultats dans hello sqlResults-trame de données pour le traçage. Voici le code de hello.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Voici des prédictions toomake de code hello et hello de traçage ROC la courbe.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**SORTIE**

![Courbe ROC de régression logistique pour une approche générique](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Conservation du modèle dans un objet blob en vue d’une consommation ultérieure**

code Hello dans cette section montre comment la régression logistique toosave hello modèle pour la consommation.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 34.57 secondes

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Utiliser la fonction pipeline CrossValidator de MLlib avec le modèle LogisticRegression (régression élastique)
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) qui prédit ou non une info-bulle est payée pour un voyage dans le jeu de données hello NYC taxi voyage et tarif. modèle de Hello est formé à l’aide de la validation croisée (VC) et hyperparameter balayage implémentées avec hello fonction de pipeline MLlib CrossValidator pour CV avec le paramètre de balayage.   

> [!NOTE]
> l’exécution de Hello de ce code MLlib CV peut prendre plusieurs minutes.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 107.98 secondes

**Tracer la courbe ROC hello.**

Hello *predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente hello. *tmp_results* peuvent être utilisés toodo requêtes et produit des résultats dans hello sqlResults-trame de données pour le traçage. Voici le code de hello.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Voici la courbe ROC hello code tooplot hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**SORTIE**

![Courbe ROC de régression logistique utilisant la fonction CrossValidator de MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Classification par forêts aléatoires
code Hello dans cette section montre comment tootrain, évaluer et enregistrer une régression de forêt aléatoire qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

Zone sous ROC = 0,985336538462

Temps nécessaire tooexecute au-dessus de la cellule : 26.72 secondes

### <a name="gradient-boosting-trees-classification"></a>Classification par arbres GBT (Gradient Boosting Tree)
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE**

Zone sous ROC = 0,985336538462

Temps nécessaire tooexecute au-dessus de la cellule : 28.13 secondes

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Prédire le montant des pourboires avec les modèles de régression (sans la validation croisée)
Cette section montre comment utiliser trois modèles pour la tâche de régression hello : prédire les temps de conseil hello payée pour un trajet taxi basé sur d’autres fonctionnalités de l’info-bulle. les modèles Hello présentées sont :

* Régression linéaire régularisée
* Forêts aléatoires
* Arbres GBT (Gradient Boosting Tree)

Ces modèles ont été décrites dans l’introduction de hello. Chaque section de code générateur de modèle est divisée en étapes : 

1. **formation du modèle** avec un jeu de paramètres
2. **Évaluation de modèle** sur un jeu de données de test avec mesures
3. **Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure   

> AZURE Remarque : La validation croisée n'est pas utilisée avec trois modèles de régression hello dans cette section, étant donné que cela a été indiqué pour les modèles de régression logistique hello en détail. Un exemple montrant comment toouse CV avec élastique Net pour la régression linéaire est fourni dans hello annexe de cette rubrique.
> 
> AZURE Remarque : Dans notre expérience, il peut avoir des problèmes avec convergence de modèles de LinearRegressionWithSGD, et les paramètres doivent toobe modifié/optimisée avec soin pour obtenir un modèle valid. La mise à l’échelle des variables est très utile avec la convergence. La régression nette élastique, indiquée dans la rubrique de toothis annexe hello, peut également servir à la place LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>régression linéaire avec SGD
Hello code dans cette section montre comment toouse à l’échelle fonctionnalités tootrain une régression linéaire qui utilise la descente de gradient stochastique (SGD) pour l’optimisation, et comment tooscore, évaluer et enregistrer le modèle de hello dans le stockage des objets Blob Azure (WASB).

> [!TIP]
> Dans notre expérience, il peut y avoir des problèmes avec convergence hello de modèles de LinearRegressionWithSGD, et les paramètres doivent toobe modifié/optimisée avec soin pour obtenir un modèle valid. La mise à l’échelle des variables est très utile avec la convergence.
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE**

Coefficients : [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]

Interception : -0,854507624459

RMSE = 1,23485131376

Racine carrée = 0,597963951127

Temps nécessaire tooexecute au-dessus de la cellule : 38.62 secondes

### <a name="random-forest-regression"></a>Régression par forêts aléatoires
code Hello dans cette section montre comment tootrain, évaluer et enregistrez un modèle de forêt aléatoire qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.   

> [!NOTE]
> La validation croisée avec à l’aide de code personnalisé de balayage des paramètres est fournie dans l’annexe de hello.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE**

RMSE = 0,931981967875

Racine carrée = 0,733445485802

Temps nécessaire tooexecute au-dessus de la cellule : 25.98 secondes

### <a name="gradient-boosting-trees-regression"></a>Régression par arbres GBT (Gradient Boosting Tree)
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.

**Former et évaluer**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

RMSE = 0,928172197114

Racine carrée = 0,732680354389

Temps nécessaire tooexecute au-dessus de la cellule : 20,9 secondes

**Tracer**

*tmp_results* est inscrit comme une table Hive dans la cellule précédente hello. Les résultats à partir de la table de hello s’affichent dans hello *sqlResults* trame de données pour le traçage. Voici le code de hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Voici hello code tooplot les données de salutation à l’aide du serveur de Notebook hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Annexe : Tâches de régression supplémentaires utilisant la validation croisée avec balayage paramétrique
Cette annexe contient l’affichage de code comment CV toodo à l’aide de net élastique pour régression linéaire et comment les CV toodo avec le paramètre de balayage à l’aide de code personnalisé pour la régression de forêt aléatoire.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Validation croisée à l’aide d’un filet élastique pour la régression linéaire
code Hello dans cette section montre comment toodo Cross-validation à l’aide d’élastique net pour la régression linéaire et comment tooevaluate hello modèle sur des données de test.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

Temps nécessaire tooexecute au-dessus de la cellule : 161.21 secondes

**Évaluer avec la mesure R-SQR**

*tmp_results* est inscrit comme une table Hive dans la cellule précédente hello. Les résultats à partir de la table de hello s’affichent dans hello *sqlResults* trame de données pour le traçage. Voici le code de hello

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Voici toocalculate de code hello sqr de R.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**SORTIE**

Racine carrée = 0,619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Validation croisée avec balayage paramétrique à l’aide de code personnalisé pour la régression par forêts aléatoires
code Hello dans cette section montre comment toodo validation croisée avec un balayage de paramètre à l’aide de code personnalisé pour la régression de forêt aléatoire, et comment tooevaluate hello modèle sur des données de test.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE**

RMSE = 0,906972198262

Racine carrée = 0,740751197012

Temps nécessaire tooexecute au-dessus de la cellule : 69.17 secondes

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Nettoyer des objets de la mémoire et imprimer les emplacements des modèles
Utilisez `unpersist()` toodelete les objets mis en mémoire cache.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**SORTIE**

PythonRDD[122] at RDD at PythonRDD.scala: 43

** Les fichiers toomodel de chemin d’accès d’impression toobe utilisé dans le bloc-notes de consommation hello. ** tooconsume et score une indépendante-jeu de données, vous devez toocopy et collez ces noms de fichiers Bonjour « Bloc-notes consommation ».

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**SORTIE**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>Et ensuite ?
Maintenant que vous avez créé des modèles de classification et de régression par hello Spark MlLib, vous êtes prêt toolearn comment tooscore et évaluer ces modèles.

**La consommation de modèle :** toolearn comment tooscore et évaluer les modèles de classification et de régression hello créés dans cette rubrique, consultez [Score et évaluer les modèles d’apprentissage automatique de Spark intégrée](machine-learning-data-science-spark-model-consumption.md).

