---
title: "aaaData exploration et de modélisation avec Spark | Documents Microsoft"
description: "Présente hello d’exploration de données et modélisation des fonctionnalités du Kit de ressources hello MLlib de Spark sur Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Exploration et modélisation des données avec Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Cette procédure pas à pas utilise l’exploration de données toodo HDInsight Spark et classification binaire et tâches sur un échantillon de hello NYC de modélisation de régression taxi voyage serrées 2013 le jeu de données.  Il vous guide à travers les étapes de hello Hello [processus de science des données](http://aka.ms/datascienceprocess), de bout en bout, à l’aide d’un HDInsight Spark cluster pour le traitement et les modèles de données et hello hello toostore d’objets BLOB Azure. processus de Hello explore et visualise les données importées à partir d’un objet Blob de stockage Azure et prépare ensuite les modèles prédictifs hello données toobuild. Ces modèles sont build à l’aide de la classification binaire du toodo toolkit Spark MLlib hello et tâches de modélisation de régression.

* Hello **classification binaire** tâche est toopredict ou non une info-bulle est payée pour le voyage de hello. 
* Hello **régression** tâche est toopredict hello Conseil hello basé sur d’autres fonctionnalités de l’info-bulle. 

Hello modèles que nous utilisons : régression logistique et linéaire, les forêts aléatoires et les arbres augmentés dégradés

* [La régression linéaire avec SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) est un modèle de régression linéaire qui utilise une méthode de descente Gradient stochastique (SGD) et pour l’optimisation et la fonctionnalité de mise à l’échelle des montants de conseil toopredict hello payé. 
* [La régression logistique avec LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou la régression « logit », est un modèle de régression qui peut être utilisé lors de la variable dépendante de hello est la classification des données catégorielles toodo. LBFGS est un algorithme d’optimisation quasi Newton qui rapproche algorithme Broyden – Fletcher – Goldfarb – Shanno (BFGS) de hello à l’aide d’une quantité limitée de mémoire de l’ordinateur, qui est largement utilisé dans l’apprentissage.
* [forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.  Combiner des nombreux decision trees tooreduce hello des risques de dépassement de. Forêts aléatoires sont utilisés pour la classification et de régression et peuvent gérer les fonctionnalités catégorielles et peuvent être étendus de paramètre de classification multiclasse toohello. Ils ne nécessitent pas la fonctionnalité mise à l’échelle et sont en mesure de toocapture non linéarité et interactions de fonctionnalité. Forêts aléatoires sont un des hello plus de succès d’apprentissage des modèles pour la classification et la régression.
* [Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision. Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte. GBTs sont utilisés pour la classification et de régression et peut gérer les fonctionnalités catégorielles, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité. Ils s’utilisent également dans le paramétrage de classification multiclasse.

étapes de modélisation Hello également contient de code montrant comment tootrain, évaluer et enregistrer chaque type de modèle. Python a été utilisé toocode hello solution et tooshow hello applique les tracés.   

> [!NOTE]
> Bien que hello Spark MLlib toolkit est conçu toowork sur les jeux de données volumineux, un exemple relativement faible (à l’aide de K 170 lignes, environ 0,1 % du jeu de données hello d’origine NYC en ~ 30 Mo) est utilisé ici pour des raisons pratiques. exercice Hello donné ici s’exécute efficacement (en environ 10 minutes) sur un cluster HDInsight avec 2 nœuds de travail. Hello même code avec des modifications mineures, peut être utilisé tooprocess-jeux de données volumineux, avec les changements appropriés pour la mise en cache des données en mémoire et la modification de la taille de cluster hello.
> 
> 

## <a name="prerequisites"></a>Composants requis
Vous avez besoin d’un compte Azure et un Spark 1.6 (ou Spark 2.0) du cluster HDInsight toocomplete cette procédure pas à pas. Consultez hello [vue d’ensemble de science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md) pour obtenir des instructions sur la façon de toosatisfy ces exigences. Cette rubrique contient également une description de type hello données NYC 2013 Taxi utilisées ici et obtenir des instructions sur la façon dont tooexecute code à partir d’un bloc-notes jupyter sur cluster Spark de hello. 

## <a name="spark-clusters-and-notebooks"></a>Clusters et notebooks Spark
Les étapes de configuration et le code fournis dans cette procédure pas à pas concernent HDInsight Spark 1.6. Mais des notebooks Jupyter sont fournis pour les clusters HDInsight Spark 1.6 et Spark 2.0. Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent. En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark. Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici. Pour des raisons pratiques, voici les liens hello blocs-notes de Notebook toohello pour Spark 1.6 (toobe exécuter dans le noyau pySpark hello Hello server de bloc-notes Jupyter) et Spark 2.0 (toobe exécuter dans le noyau pySpark3 hello Hello server de bloc-notes Jupyter) :

### <a name="spark-16-notebooks"></a>Notebooks Spark 1.6

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fournit des informations sur l’exploration de données tooperform, de modélisation et de calcul de score avec plusieurs algorithmes différents.

### <a name="spark-20-notebooks"></a>Notebooks Spark 2.0
tâches de classification et de régression Hello qui sont implémentées à l’aide d’un cluster Spark 2.0 se trouvent dans les blocs-notes et portable de classification hello utilise un autre jeu de données :

- [Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ce fichier fournit des informations sur comment tooperform l’exploration de données, de modélisation et de calcul de score dans Spark 2.0 des clusters à l’aide de hello voyage de NYC Taxi et tarif-jeu de données décrit [ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Cet ordinateur portable peut être un bon point de départ pour Explorer rapidement le code de hello que nous fournissons à Spark 2.0. Pour un ordinateur portable plu analyse hello les données NYC Taxi, consultez bloc-notes suivant de hello dans cette liste. Consultez les remarques hello suit cette liste qui comparent ces ordinateurs portables. 
- [Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): ce fichier montre comment tooperform données ensuivirent (opérations Spark SQL et de la trame de données), exploration, de modélisation et de calcul de score à l’aide de hello voyage de NYC Taxi et tarif de jeu de données décrites [ ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): ce fichier montre comment tooperform données ensuivirent (opérations Spark SQL et de la trame de données), exploration, de modélisation et de calcul de score à l’aide de hello connu départ à temps de billet d’avion jeu de données à partir de 2011 et 2012. Nous l’intégration hello compagnie aérienne dataset avec hello aéroport météo (par exemple, vitesse du vent, la température, altitude, etc.) de données préalable toomodeling, ces fonctionnalités météo peuvent être incluses dans le modèle de hello.

<!-- -->

> [!NOTE]
> Hello compagnie aérienne dataset a été ajouté toohello Spark 2.0 blocs-notes toobetter illustrer l’utilisation de hello des algorithmes de classification. Consultez hello suivant les liens pour plus d’informations sur le jeu de données de départ de délais compagnie aérienne et jeu de données météo :

>- Données sur les départs à l’heure des compagnies aériennes : [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Données météorologiques des aéroports : [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
ordinateurs portables de Spark 2.0 Hello sur hello taxi de NYC et compagnie aérienne flight delay-jeux de données peuvent prendre 10 minutes ou plus toorun (selon la taille de votre cluster HDI de hello). Hello premier bloc-notes Bonjour au-dessus de liste affiche nombreux aspects d’exploration de données hello, ML de visualisation et de modèle d’apprentissage dans un ordinateur portable qui prend moins toorun temps avec échantillonnées en bas NYC jeu de données, dans quel hello taxi et tarif de fichiers ont été déjà joints : [ Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) ce bloc-notes prend une quantité plus court toofinish de temps (2 à 3 minutes) et peut être un bon point de départ pour Explorer rapidement le code de hello nous avons fourni pour Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
descriptions Hello suivantes sont associée toousing Spark 1.6. Pour les versions Spark 2.0, utilisez les blocs-notes hello décrite et lien indiqué plus haut. 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Importer les bibliothèques
Le programme d’installation nécessite également l’importation des bibliothèques nécessaires. Définir le contexte de spark et importer des bibliothèques nécessaires avec hello suivant de code :

    # IMPORT LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>Ingestion de données à partir d’un objet blob public
première étape de Hello dans le processus de science des données hello est tooingest hello données toobe analysée à partir de sources d’où est réside dans votre environnement de modélisation et exploration de données. environnement de Hello est Spark dans cette procédure pas à pas. Cette section contient des toocomplete de code hello une série de tâches :

* réception hello données exemple toobe modélisée
* lire dans le jeu de données d’entrée hello (stockée sous la forme d’un fichier .tsv)
* format et hello nettoyer les données
* créer et mettre en cache des objets (RDD ou trames de données) en mémoire
* enregistrer les données en tant que table temporaire dans le contexte SQL.

Voici le code hello pour l’ingestion de données.

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 51.72 secondes

## <a name="data-exploration--visualization"></a>Exploration et visualisation de données
Une fois les données de salutation a été placées dans Spark, hello étape suivante dans le processus de science des données hello est toogain une meilleure compréhension des données hello via l’exploration et visualisation. Dans cette section, nous examiner les données de taxi hello à l’aide de requêtes SQL et des variables de traçage hello cibles et des fonctionnalités potentiels pour l’examen visuel. Plus précisément, nous tracer fréquence hello passagers des nombres de dans taxi allers-retours, hello fréquence de quantités d’info-bulle, et comment les conseils varient selon le type et le montant du paiement.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Tracer un histogramme de fréquences d’inventaire passagers dans l’exemple hello de déplacements de taxi
Ce code et les extraits de code suivants utilisent SQL tooquery magique hello, exemple et les données de hello de tooplot magique local.

* **Magique SQL (`%%sql`)** hello HDInsight PySpark noyau prend en charge easy inline HiveQL requêtes contre hello sqlContext. Hello (-o nom_variable) argument persiste sortie hello de la requête SQL hello en tant qu’une trame de données Pandas sur le serveur de Notebook hello. Cela signifie qu’il est disponible en mode local de hello.
* Hello  **`%%local` magique** est toorun du code utilisé localement sur le serveur hello Notebook, qui est le nœud principal de hello du cluster HDInsight de hello. En général, vous utilisez `%%local` magique conjointement avec hello `%%sql` magique avec le paramètre -o. paramètre de Hello -o soit persistant sortie hello de requête SQL hello localement, puis %% magic local déclencherait hello prochain jeu de toorun d’extrait de code localement par rapport à la sortie hello de requêtes SQL hello rendue persistante localement

Hello sortie est automatiquement affichée après l’exécution de code de hello.

Cette requête extrait les allers-retours hello par nombre de passagers. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Ce code crée une trame de données locale à partir de la sortie de la requête hello et trace les données de salutation. Hello `%%local` magique crée une trame de données locale, `sqlResults`, qui peut être utilisé pour le traçage avec matplotlib. 

> [!NOTE]
> Cette commande magique PySpark est utilisée plusieurs fois lors de cette procédure pas à pas. Si la quantité de hello de données est importante, vous devez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Voici allers-retours de hello hello code tooplot par passager nombres

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**SORTIE :**

![Fréquence des voyages par nombre de passagers](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

Vous pouvez sélectionner parmi les différents types de visualisations (Table, à secteurs, ligne, zone ou barre) à l’aide de hello **Type** des boutons de menu dans le bloc-notes de hello. traçage de barre Hello est indiqué ici.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Tracez un histogramme du montant des pourboires et montrez comment le montant du pourboire varie selon le nombre de passagers et le montant des trajets.
Utilisez une données toosample de requête SQL.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**SORTIE :** 

![Distribution des montants de pourboire](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Conception des caractéristiques, transformation et préparation des données à modéliser
Cette section décrit et fournit le code hello pour les procédures utilisées tooprepare données pour une utilisation dans la modélisation de ML. Il montre des tâches de hello toodo suivant :

* Créer une caractéristique en regroupant les heures dans des périodes de trafic
* Indexer et encoder des fonctionnalités catégorielles
* Créer des objets point étiquetés à intégrer dans les fonctions ML
* Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test
* Mise à l’échelle des caractéristiques
* Mettre en cache des objets en mémoire

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Créer une caractéristique en regroupant les heures dans des périodes de trafic
Ce code montre comment les compartiments de toocreate une nouvelle fonctionnalité par le placement des heures dans le temps de trafic, puis comment toocache hello résultant trame de données en mémoire. Où résilient Distributed jeux de données (RDDs) et les trames de données sont utilisés à plusieurs reprises, mise en cache entraîne des temps d’exécution tooimproved. En conséquence, nous le cache RDDs trames de données à plusieurs étapes dans la procédure pas à pas hello. 

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

**SORTIE :** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Indexer et encoder les caractéristiques catégorielles à intégrer dans les fonctions de modélisation
Cette section montre comment tooindex ou coder des fonctionnalités par catégorie pour l’entrée en hello modélisation des fonctions. modélisation de Hello et prédire les fonctions de MLlib requièrent des fonctionnalités avec les données d’entrée catégorielles toobe indexé ou codé toouse préalable. Selon le modèle de hello, tooindex ou que vous les codez de différentes façons :  

* **Basé sur l’arborescence de modélisation** requiert toobe catégories encodé sous la forme des valeurs numériques (par exemple, une fonctionnalité avec trois catégories peut-être être encodée avec 0, 1, 2). C’est ce que permet la fonction [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) de MLlib. Cette fonction encode une colonne de chaîne de colonne d’étiquettes de tooa d’indices d’étiquette qui sont classés par fréquence d’étiquette. Bien qu’il est indexé par des valeurs numériques pour l’entrée et la gestion des données, les algorithmes d’arbre hello peuvent être spécifié tootreat leur correctement en tant que catégories. 
* **Modèles de logistique et de régression linéaire** requièrent à chaud de celui de codage, où, par exemple, une fonctionnalité avec trois catégories peut être développée dans les trois colonnes de fonctionnalités, avec chaque conteneur 0 ou 1 selon la catégorie hello d’une observation. Fournit des MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo à chaud un encodage de la fonction. Cet encodeur est mappé à une colonne de la colonne de tooa étiquette indices de vecteurs binaire, au maximum une seule une valeur. Cet encodage permet d’algorithmes qui attendent des fonctionnalités de valeurs numériques, telles que la régression logistique, fonctionnalités de toocategorical toobe appliqué.

Voici hello code tooindex et coder les fonctionnalités par catégorie :

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 1,28 secondes

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Créer des objets point étiquetés à intégrer dans les fonctions ML
Cette section contient le code qui montre comment les données de texte catégorielles tooindex au point étiqueté les données de type et coder afin qu’il puisse être utilisé tootrain et test MLlib régression logistique et autres modèles de classification. Les objets point étiquetés sont des jeux de données distribués résilients (RDD) mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes ML dans MLlib. Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.  

Cette section contient le code qui montre comment tooindex les données de texte par catégorie comme un [intitulée point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) type de données et les encoder afin qu’il puisse être utilisé tootrain et test MLlib régression logistique et autres modèles de classification. Les objets point étiquetés sont des jeux de données distribués résilients (RDD) composés d’un libellé (variable cible/réponse) et du vecteur de caractéristique. Ce format est nécessaire en entrée par de nombreux algorithmes ML de MLlib.

Voici hello tooindex de code et de coder des fonctionnalités de texte pour la classification binaire.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
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
Ce code crée un échantillonnage aléatoire de données hello (25 % est utilisé ici). Bien qu’il n’est pas requis pour cet exemple en raison de la taille de toohello du jeu de données hello, nous allons montrer comment vous pouvez échantillonner ici afin de savoir comment toouse pour votre propre problème si nécessaire. Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles. Ensuite, nous fractionner les exemple hello en une partie de la formation (75 % ici) et un test toouse de partie (25 % ici) dans la classification et la modélisation de régression.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : pas de 0,24 secondes

### <a name="feature-scaling"></a>Mise à l’échelle des caractéristiques
Fonctionnalité mise à l’échelle, également appelé normalisation des données, ainsi que des fonctionnalités avec des valeurs largement dispersées sont pas donné excessive peser en fonction de l’objectif hello. code de mise à l’échelle d’une fonctionnalité Hello utilise hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variance de toounit fonctionnalités tooscale hello. MLlib le fournit en vue d’une utilisation dans une régression linéaire avec SGD (Stochastic Gradient Descent), un algorithme populaire permettant de former une large gamme d’autres modèles Machine Learning, tels que les régressions régularisées ou les machines à vecteurs de support (SVM).

> [!NOTE]
> Nous avons trouvé hello LinearRegressionWithSGD algorithme toobe toofeature sensibles mise à l’échelle.
> 
> 

Voici les variables de tooscale code hello pour une utilisation avec l’algorithme SGD hello régularisée linéaire.

    # FEATURE SCALING

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

**SORTIE :**

Temps nécessaire tooexecute au-dessus de la cellule : 13.17 secondes

### <a name="cache-objects-in-memory"></a>Mettre en cache des objets en mémoire
Hello temps d’apprentissage et test des algorithmes de ML peuvent être réduits en mettant en cache des objets d’image de données d’entrée hello utilisés pour la classification, la régression, et les fonctionnalités de mise à l’échelle.

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

**SORTIE :** 

Temps nécessaire tooexecute au-dessus de la cellule : secondes environ 0,15

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Prédire si un pourboire a été payé avec des modèles de classification binaires
Cette section montre comment utiliser trois modèles pour la tâche de classification binaire hello de prédiction ou non une info-bulle est payée pour un voyage taxi. les modèles Hello présentées sont :

* Régression logistique régularisée 
* Modèle de forêts aléatoires
* Arbres GBT (Gradient Boosting Tree)

Chaque section de code générateur de modèle est divisée en étapes : 

1. **formation du modèle** avec un jeu de paramètres
2. **Évaluation de modèle** sur un jeu de données de test avec mesures
3. **Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure

### <a name="classification-using-logistic-regression"></a>Classification par régression logistique
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) qui prédit ou non une info-bulle est payée pour un voyage dans le jeu de données hello NYC taxi voyage et tarif.

**L’apprentissage du modèle de régression logistique hello à l’aide de CV et hyperparameter balayage**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SORTIE :** 

Coefficients : [0,0082065285375, -0,0223675576104, -0,0183812028036, -3.48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]

Interception : -0,0111216486893

Temps nécessaire tooexecute au-dessus de la cellule : 14.43 secondes

**Évaluation du modèle de classification binaire hello avec métriques standard**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SORTIE :** 

Zone sous PR = 0,985297691373

Zone sous ROC = 0,983714670256

Résumé des statistiques

Précision = 0,984304060189

Rappel = 0,984304060189

Score F1 = 0,984304060189

Temps nécessaire tooexecute au-dessus de la cellule : 57.61 secondes

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

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


**SORTIE :**

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Classification par forêts aléatoires
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de forêt aléatoire qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

**SORTIE :**

Zone sous ROC = 0,985297691373

Temps nécessaire tooexecute au-dessus de la cellule : 31.09 secondes

### <a name="gradient-boosting-trees-classification"></a>Classification par arbres GBT (Gradient Boosting Tree)
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


**SORTIE :**

Zone sous ROC = 0,985297691373

Temps nécessaire tooexecute au-dessus de la cellule : 19.76 secondes

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Prédire le montant des pourboires de courses de taxi avec les modèles de régression
Cette section montre comment utiliser trois modèles pour la tâche de régression hello de prévoir hello de conseil hello payée pour un trajet taxi basé sur d’autres fonctionnalités de l’info-bulle. les modèles Hello présentées sont :

* Régression linéaire régularisée
* Forêts aléatoires
* Arbres GBT (Gradient Boosting Tree)

Ces modèles ont été décrites dans l’introduction de hello. Chaque section de code générateur de modèle est divisée en étapes : 

1. **formation du modèle** avec un jeu de paramètres
2. **Évaluation de modèle** sur un jeu de données de test avec mesures
3. **Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure

### <a name="linear-regression-with-sgd"></a>régression linéaire avec SGD
Hello code dans cette section montre comment toouse à l’échelle fonctionnalités tootrain une régression linéaire qui utilise la descente de gradient stochastique (SGD) pour l’optimisation, et comment tooscore, évaluer et enregistrer le modèle de hello dans le stockage des objets Blob Azure (WASB).

> [!TIP]
> Dans notre expérience, il peut y avoir des problèmes avec convergence hello de modèles de LinearRegressionWithSGD, et les paramètres doivent toobe modifié/optimisée avec soin pour obtenir un modèle valid. La mise à l’échelle des variables est très utile avec la convergence. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE :**

Coefficients : [0,00457675809917, -0,0226314167349, -0,0191910355236, 0,246793409578, 0,312047890459, 0,359634405999, 0,00928692253981, -0,000987181489428, -0,0888306617845, 0,0569376211553, 0,115519551711, 0,149250164995, -0,00990211159703, -0,00637410344522, 0,545083566179, -0,536756072402, 0,0105762393099, -0,0130117577055, 0,0129304737772, -0,00171065945959]

Interception : -0,853872718283

RMSE = 1,24190115863

Racine carrée = 0,608017146081

Temps nécessaire tooexecute au-dessus de la cellule : 58,42 secondes

### <a name="random-forest-regression"></a>Régression par forêts aléatoires
code Hello dans cette section montre comment tootrain, évaluer et enregistrer une régression de forêt aléatoire qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

**SORTIE :**

RMSE = 0,891209218139

Racine carrée = 0,759661334921

Temps nécessaire tooexecute au-dessus de la cellule : 49.21 secondes

### <a name="gradient-boosting-trees-regression"></a>Régression par arbres GBT (Gradient Boosting Tree)
code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.

**Former et évaluer**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SORTIE :**

RMSE = 0,908473148639

Racine carrée = 0,753835096681

Temps nécessaire tooexecute au-dessus de la cellule : 34.52 secondes

**Tracer**

*tmp_results* est inscrit comme une table Hive dans la cellule précédente hello. Les résultats à partir de la table de hello s’affichent dans hello *sqlResults* trame de données pour le traçage. Voici le code de hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Voici hello code tooplot les données de salutation à l’aide du serveur de Notebook hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**SORTIE :**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Nettoyage d’objets de la mémoire
Utilisez `unpersist()` toodelete les objets mis en mémoire cache.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Enregistrement des emplacements de stockage des modèles de hello pour la consommation et le score
tooconsume et score un jeu de données indépendant décrit dans hello [Score et évaluer des modèles d’apprentissage automatique intégrée Spark](machine-learning-data-science-spark-model-consumption.md) rubrique, vous devez toocopy et coller contenant hello enregistré les modèles créés ici dans hello des noms de ces fichiers Bloc-notes jupyter de consommation. Voici tooprint de code hello out hello chemins toomodel fichiers que vous devez il.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**SORTIE**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>Et ensuite ?
Maintenant que vous avez créé des modèles de classification et de régression par hello Spark MlLib, vous êtes prêt toolearn comment tooscore et évaluer ces modèles. Bonjour avancé d’exploration de données et de modélisation tels que le bloc-notes plus approfondie en y compris la validation croisée, hyper-paramètre de balayage des et d’évaluation de modèle. 

**La consommation de modèle :** toolearn comment tooscore et évaluer les modèles de classification et de régression hello créés dans cette rubrique, consultez [Score et évaluer les modèles d’apprentissage automatique de Spark intégrée](machine-learning-data-science-spark-model-consumption.md).

**Validation croisée et balayage hyperparamétrique**: consultez [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment effectuer la formation des modèles à l’aide de la validation croisée et du balayage hyperparamétrique

