---
title: "aaaData Science à l’aide de Scala et Spark sur Azure | Documents Microsoft"
description: "Comment toouse Scala pour les tâches à l’aide d’apprentissage supervisé hello Spark MLlib et Spark ML packages évolutifs sur un cluster Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Science des données à l’aide de Scala et Spark sur Azure
Cet article vous explique comment toouse Scala pour les tâches d’apprentissage automatique supervisé avec hello MLlib évolutive de Spark et Spark ML packages sur un cluster Azure HDInsight Spark. Il vous guide à travers les tâches hello constituant hello [processus de science des données](http://aka.ms/datascienceprocess): intégrer les données et exploration, de visualisation, l’ingénierie de fonctionnalité, modélisation et la consommation de modèle. les modèles de Hello dans l’article de hello incluent la régression logistique et linéaire, les forêts aléatoires et les arbres augmentés de dégradé (GBTs), en outre tootwo commun supervisé tâches d’apprentissage automatique :

* Problème de régression : prédiction du montant de conseil hello ($) pour un voyage taxi
* Classification binaire : prédiction de la réception d’un pourboire ou non (1/0) pour une course en taxi

Hello, processus de modélisation requiert la formation et évaluation sur un jeu de données de test et les mesures de précision pertinentes. Dans cet article, vous pouvez apprendre comment toostore ces modèles dans le stockage Blob Azure et comment tooscore et d’évaluer leurs performances prédictive. Cet article couvre également hello plus avancée des rubriques Comment toooptimize modèles à l’aide de la validation croisée et hyper-paramètre de balayage. les données de salutation utilisées sont un exemple hello 2013 NYC taxi voyage et le prix du jeu de données disponible sur GitHub.

[Scala](http://www.scala-lang.org/), un langage basé sur une machine virtuelle hello, intègre les concepts de langage fonctionnelle et orientée objet. Il est un langage évolutif est parfaitement adaptée toodistributed de traitement dans le cloud de hello et s’exécute sur les clusters Azure Spark.

[Spark](http://spark.apache.org/) est une infrastructure de traitement parallèle open source qui prend en charge en mémoire traitement tooboost les performances de hello big applications de données analytique. moteur de traitement Spark Hello est créé pour la vitesse, la facilité d’utilisation et analytique sophistiquées. De par ses capacités de calcul distribué en mémoire, Spark constitue le choix idéal pour les algorithmes itératifs utilisés dans l'apprentissage automatique et les calculs de graphiques. Hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package fournit un ensemble cohérent de haut niveau API reposant sur des données d’images qui peuvent vous aider à créer et analyser les pipelines d’apprentissage pratique. [MLlib](http://spark.apache.org/mllib/) est la bibliothèque de Spark apprentissage évolutif, qui offre des fonctionnalités de modélisation toothis des environnement distribué.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) est hello hébergés par Azure offre d’open source Spark. Il inclut également la prise en charge pour les ordinateurs portables Jupyter Scala sur cluster Spark de hello et pouvez exécution tootransform de requêtes interactif Spark SQL, filtrer et visualiser les données stockées dans le stockage Blob Azure. Hello Scala extraits de code dans cet article qui fournissent des solutions de hello et affichent les graphiques appropriés hello toovisualize les données de salutation s’exécutent dans les blocs-notes Notebook installés sur des clusters de Spark hello. étapes de modélisation Hello dans ces rubriques ont du code qui s’affiche vous comment tootrain, évaluer, enregistrer et utiliser chaque type de modèle.

étapes de configuration Hello et de code dans cet article sont destinées Azure HDInsight 3.4 Spark 1.6. Toutefois, hello code dans cet article et hello [Scala bloc-notes Jupyter](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) sont génériques et doit fonctionner sur n’importe quel cluster Spark. Hello le programme d’installation de cluster et les étapes de gestion peuvent être légèrement différentes de ce qui est affiché dans cet article, si vous n’utilisez pas HDInsight Spark.

> [!NOTE]
> Pour une rubrique qui vous montre comment toocomplete de Python plutôt que Scala toouse tâches pour un processus de science des données de bout en bout, consultez [Science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Composants requis
* Vous devez avoir un abonnement Azure. Si vous n’en avez pas, [obtenez une version d’évaluation gratuite Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Vous avez besoin d’un hello toocomplete de cluster Azure HDInsight 3.4 Spark 1.6 procédures suivantes. toocreate un cluster, consultez les instructions de hello dans [mise en route : créer Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Définir le type de cluster hello et la version sur hello **sélectionner le Type de Cluster** menu.

![Configuration de type cluster HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Pour obtenir une description des données de voyage hello NYC taxi et obtenir des instructions sur la façon dont tooexecute code à partir d’un bloc-notes jupyter sur cluster Spark de hello, consultez les sections pertinentes de hello dans [vue d’ensemble de science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Exécute un bloc-notes jupyter sur cluster Spark de hello Scala du code
Vous pouvez lancer un bloc-notes jupyter de hello portail Azure. Recherchez le cluster Spark de hello sur votre tableau de bord, puis cliquez sur page de gestion tooenter hello pour votre cluster. Ensuite, cliquez sur **tableaux de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter** bloc-notes de hello tooopen associé hello Spark cluster.

![Tableau de bord de cluster et notebooks Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

Vous pouvez également accéder aux notebooks Jupyter à l’adresse https://&lt;clustername&gt;.azurehdinsight.net/jupyter. Remplacez *clustername* avec nom hello de votre cluster. Vous avez besoin d’un mot de passe hello pour vos blocs-notes Notebook hello de tooaccess de compte administrateur.

![Accédez tooJupyter portables à l’aide du nom du cluster hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Sélectionnez **Scala** toosee un répertoire avec quelques exemples d’ordinateurs portables préconfigurées que hello utilisation PySpark API. Hello score et modélisation de l’Exploration à l’aide du bloc-notes Scala.ipynb qui contient des exemples de code hello pour cet ensemble de rubriques de Spark est disponible sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

Vous pouvez télécharger le bloc-notes hello directement à partir de GitHub toohello server de bloc-notes Jupyter sur votre cluster Spark. Sur votre page d’accueil Notebook, cliquez sur hello **télécharger** bouton. Dans l’Explorateur de fichiers hello, collez hello les URL de GitHub (contenu brut) de l’ordinateur portable de hello Scala, puis cliquez sur **ouvrir**. ordinateur portable de Scala Hello est disponible à hello suivant l’URL :

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Configuration : contextes Spark et Hive prédéfinis, commandes magiques Spark et bibliothèques Spark
### <a name="preset-spark-and-hive-contexts"></a>Contextes Spark et Hive prédéfinis
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


les noyaux Spark Hello qui sont fournis avec les ordinateurs portables Notebook ont contextes prédéfinis. Vous n’avez pas besoin tooexplicitly ensemble hello Spark ou Hive contextes avant de commencer à utiliser avec l’application hello que vous développez. Hello contextes prédéfinis sont :

* `sc` pour SparkContext
* `sqlContext` pour HiveContext

### <a name="spark-magics"></a>Commandes magiques de Spark
Hello Spark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec `%%`. Deux de ces commandes sont utilisées dans hello suivant des exemples de code.

* `%%local`Spécifie que le code hello dans les lignes suivantes sera exécuté localement. code de Hello doit être code Scala valide.
* `%%sql -o <variable name>` exécute une requête Hive sur `sqlContext`. Si hello `-o` paramètre est passé, résultat hello de requête de hello est conservée dans hello `%%local` contexte Scala en tant qu’une trame de données Spark.

Pour plus d’informations sur les noyaux hello Notebook blocs-notes et leurs prédéfinie « magics » que vous appelez avec `%%` (par exemple, `%%local`), consultez [noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur les clusters HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Importer les bibliothèques
Importer hello Spark, MLlib et autres bibliothèques que vous aurez besoin à l’aide de hello suivant de code.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Ingestion de données
première étape de Hello Bonjour processus de science des données donnée tooingest hello que vous souhaitez tooanalyze. Vous récupérez des données de hello à partir de sources externes ou des systèmes où il réside dans votre environnement de modélisation et exploration de données. Dans cet article, les données de salutation que vous réception sont un exemple de 0,1 % jointes hello taxi voyage et le prix du fichier de (stocké sous forme de fichier .tsv). environnement de modélisation et exploration de données Hello est Spark. Cette section contient hello de toocomplete code hello après la série de tâches :

1. Définir les chemins d’accès pour le stockage des données et du modèle.
2. Lire dans hello jeu de données d’entrée (stockée sous la forme d’un fichier .tsv).
3. Définir un schéma pour les données hello et nettoyer hello.
4. Créer une trame de données propre, puis la mettre en mémoire cache.
5. Enregistrer les données de salutation comme une table temporaire dans SQLContext.
6. Interroger la table de hello et importer les résultats de hello dans une trame de données.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Définir les chemins d’accès aux emplacements de stockage dans le stockage d’objets blob Azure.
Spark peut lire et écrire des tooAzure stockage d’objets Blob. Vous pouvez utiliser Spark tooprocess vos données existantes et puis stocker les résultats de hello à nouveau dans le stockage Blob.

modèles de toosave ou les fichiers dans le stockage Blob, vous devez tooproperly spécifier le chemin d’accès hello. Conteneur par défaut de hello référence jointe cluster Spark de toohello à l’aide d’un chemin d’accès qui commence par `wasb:///`. Référencez d’autres emplacements en utilisant `wasb://`.

Hello exemple de code suivant spécifie emplacement hello de hello toobe de données d’entrée en lecture et un stockage tooBlob hello chemin d’accès qui est attaché toohello Spark cluster où le modèle de hello sera enregistrée.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Importer des données, créer un RDD et définir une trame de données selon le schéma de toohello
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cellule de temps toorun hello : 8 secondes.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Interroger la table de hello et importer les résultats dans une trame de données
Ensuite, table des requêtes hello des prix, les passagers et les données de l’info-bulle ; filtrer les données endommagées et américaines ; et imprimer plusieurs lignes.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Output:**

| fare_amount | passenger_count | tip_amount | tipped |
| --- | --- | --- | --- |
|        13,5 |1.0 |2,9 |1.0 |
|        16,0 |2.0 |3.4 |1.0 |
|        10,5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Exploration et visualisation de données
Une fois que vous importez des données de salutation dans Spark, étape suivante hello hello processus de science des données est toogain une meilleure compréhension des données hello via l’exploration et visualisation. Dans cette section, vous examinez les données de salutation taxi à l’aide de requêtes SQL. Ensuite, importer les résultats dans un tooplot de trame de données hello hello variables cibles et des fonctionnalités potentiels pour l’examen visuel par à l’aide de la fonctionnalité de visualisation automatique hello du bloc-notes.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Utilisez local et tooplot magique de données SQL
Par défaut, la sortie hello de tout extrait de code que vous exécutez à partir d’un bloc-notes jupyter est disponible dans le contexte de hello de session hello qui est rendues persistantes sur les nœuds de travail hello. Si vous voulez toosave un toohello de nœuds de travail voyage pour chaque calcul, et que si tous les hello les données dont vous avez besoin pour votre calcul est disponible localement sur le nœud du serveur hello Notebook (qui est le nœud principal de hello), vous pouvez utiliser hello `%%local` magique code hello de toorun extrait de code sur le serveur de Notebook hello.

* **Commande magique SQL** (`%%sql`). Hello du noyau de HDInsight Spark prend en charge les requêtes de HiveQL d’inline facile contre SQLContext. Hello (`-o VARIABLE_NAME`) argument persiste sortie hello de la requête SQL hello en tant qu’une trame de données Pandas sur le serveur de Notebook hello. Cela signifie qu'est disponible en mode local de hello.
* `%%local`**Commande magique**. Hello `%%local` magique exécute le code de hello localement sur le serveur hello Notebook, qui est le nœud principal de hello du cluster HDInsight de hello. En général, vous utilisez `%%local` magique conjointement avec hello `%%sql` magique avec hello `-o` paramètre. Hello `-o` paramètre soit persistant sortie hello de requête SQL hello localement, puis `%%local` magique déclencherait hello prochain jeu de toorun d’extrait de code localement par rapport à la sortie hello de requêtes SQL hello qui est conservé localement.

### <a name="query-hello-data-by-using-sql"></a>Hello interroger des données à l’aide de SQL
Cette requête extrait des boucles de taxi hello par montant de frais, nombre de passagers et quantité d’info-bulle.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

Bonjour suivant de code, hello `%%local` magique crée une trame de données local, sqlResults. Vous pouvez utiliser sqlResults tooplot à l’aide de matplotlib.

> [!TIP]
> Cette commande magique locale est utilisée plusieurs fois dans cet article. Si votre jeu de données est volumineuse, veuillez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.
> 
> 

### <a name="plot-hello-data"></a>Tracer les données hello
Vous pouvez tracer à l’aide de code Python après de la trame de données hello est dans le contexte local en tant qu’une trame de données Pandas.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 noyau de Spark Hello visualise automatiquement sortie hello des requêtes SQL (HiveQL) après l’exécution de code de hello. Vous pouvez choisir entre plusieurs types de visualisations :

* Table
* Secteurs
* Lignes
* Domaine
* Barres

Voici les données de salutation tooplot hello code :

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Output:**

![Histogramme de montant de pourboire](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Créer des fonctions et fonctionnalités de transformation puis préparer les données à intégrer dans les fonctions de modélisation
Pour les fonctions de modélisation basés sur l’arborescence à partir de Spark ML et MLlib, vous avez tooprepare cible et des fonctionnalités à l’aide de diverses techniques, telles que le placement, l’indexation, à chaud de celui de codage et vectorisation. Voici hello procédures toofollow dans cette section :

1. Créer une caractéristique en **regroupant** les heures dans des périodes de trafic
2. Appliquer **l’indexation et l’encodage à chaud de celui** toocategorical fonctionnalités.
3. **Échantillonner et fractionner hello jeu de données** en fractions d’apprentissage et de test.
4. **Spécifier la variable de formation et les fonctionnalités**, puis créer des jeux de données distribués résilients (RDD) ou trames de données d’entrée libellés de formation et de test indexés ou encodés à chaud
5. Automatiquement **classer et vectoriser les fonctionnalités et les cibles** toouse en tant qu’entrées pour les modèles d’apprentissage automatique.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Créer une caractéristique en regroupant les heures dans des périodes de trafic
Ce code montre comment les compartiments de toocreate une nouvelle fonctionnalité par le placement des heures dans le temps de trafic et comment toocache hello résultant trame de données en mémoire. Lorsque les frames RDDs et les données sont utilisés à plusieurs reprises, la mise en cache entraîne des temps d’exécution tooimproved. En conséquence, vous allez mettre en cache les frames RDDs et les données à plusieurs stades Bonjour procédures suivantes.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Indexation et encodage « à chaud » des fonctionnalités catégorielles
modélisation de Hello et prédire les fonctions de MLlib requièrent des fonctionnalités avec les données d’entrée catégorielles toobe indexé ou codé toouse préalable. Cette section vous montre comment tooindex ou coder des fonctionnalités par catégorie pour l’entrée en hello modélisation des fonctions.

Vous devez tooindex ou coder vos modèles de différentes façons, selon le modèle de hello. Par exemple, les modèles de régression logistique et linéaire nécessitent un encodage « à chaud ». Par exemple, une fonction avec trois catégories peut être étendue sur trois colonnes de fonctionnalités. Chaque colonne contient 0 ou 1 selon la catégorie hello d’une observation. MLlib fournit hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) fonction pour à chaud de celui de codage. Cet encodeur est mappé à une colonne de la colonne de tooa étiquette indices de vecteurs binaire au maximum une seule une valeur. Cet encodage, les algorithmes qui attendent des fonctionnalités de valeurs numériques, telles que la régression logistique, peuvent être appliqué toocategorical fonctionnalités.

Ici, vous transformez uniquement quatre variables tooshow obtenir des exemples, qui sont des chaînes de caractères. Vous pouvez également indexer d’autres variables, telles que le jour de la semaine, représentées par des valeurs numériques, en tant que variables catégorielles.

Pour l’indexation, utilisez `StringIndexer()`, et pour l’encodage « à chaud », utilisez les fonctions `OneHotEncoder()` de MLlib. Voici hello code tooindex et coder les fonctionnalités par catégorie :

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cellule de temps toorun hello : 4 secondes.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Échantillonner et fractionner hello le jeu de données en fractions d’apprentissage et de test
Ce code crée un échantillonnage aléatoire de données de salutation (25 %, dans cet exemple). Bien qu’il n’est pas requis pour cet exemple en raison de la taille de toohello hello du jeu de données, hello explique également comment vous pouvez échantillonner afin que vous sachiez comment toouse pour vos propres problèmes si nécessaire. Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles. Ensuite, fractionner exemple hello en une partie de la formation (dans cet exemple, 75 %) et un test partie toouse (25 %, dans cet exemple) dans la classification et la modélisation de régression.

Ajoutez une ligne tooeach nombre aléatoire (entre 0 et 1) (dans une colonne « rand ») qui peut être des plis de validation croisée tooselect utilisés pendant la formation.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cellule de temps toorun hello : 2 secondes.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Spécifiez la variable de formation et les fonctionnalités puis créez des objets RDD ou trames de données d’entrée libellés de formation et de test indexés ou encodés à chaud.
Cette section contient le code qui vous montre comment tooindex les données de texte par catégorie comme un étiqueté pointent le type de données et comment l’encoder afin de pouvoir utiliser tootrain et test de régression logistique MLlib et d’autres modèles de classification. Les objets point étiquetés sont des RDD mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes Machine Learning dans MLlib. Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.

Dans ce code, vous spécifiez la variable de hello cible (dépendante) et hello fonctionnalités toouse tootrain des modèles. Vous créez ensuite des objets RDD ou trames de données d’entrée libellés de formation et de test indexés ou encodés à chaud.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cellule de temps toorun hello : 4 secondes.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Classer automatiquement et de vectoriser toouse des fonctionnalités et des cibles en tant qu’entrées pour les modèles d’apprentissage automatique
Utiliser Spark ML toocategorize hello cible et les fonctionnalités toouse dans les fonctions de modélisation basés sur l’arborescence. code de Hello effectue deux tâches :

* Crée une binaire cible pour la classification en affectant la valeur 0 ou 1 point de données tooeach comprise entre 0 et 1 à l’aide d’une valeur de seuil de 0,5.
* Classe automatiquement les fonctionnalités. Si nombre hello de distinctes des valeurs numériques pour n’importe quelle fonctionnalité est inférieure à 32, cette fonctionnalité est classée.

Voici le code hello pour ces deux tâches.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Modèle de classification binaire : Prédire si un pourboire doit être payé ou non
Dans cette section, vous créez trois types de toopredict de modèles de classification binaire ou non une info-bulle doit être accordée :

* A **modèle de régression logistique** à l’aide de hello Spark ML `LogisticRegression()` (fonction)
* A **modèle de classification de forêt aléatoire** à l’aide de hello Spark ML `RandomForestClassifier()` (fonction)
* A **modèle de classification d’un arbre de renforcement dégradé** à l’aide de hello MLlib `GradientBoostedTrees()` (fonction)

### <a name="create-a-logistic-regression-model"></a>Créer un modèle de régression logistique
Ensuite, créez un modèle de régression logistique à l’aide de hello Spark ML `LogisticRegression()` (fonction). Vous créez le modèle hello génération de code dans une série d’étapes :

1. **Modèle de hello train** données avec un jeu de paramètres.
2. **Évaluation du modèle de hello** sur un jeu de données de test avec les mesures.
3. **Enregistrer le modèle de hello** dans le stockage Blob de sa consommation ultérieure.
4. **Modèle de score hello** par rapport aux données de test.
5. **Tracer les résultats hello** avec récepteur courbes de caractéristique (ROC).

Voici le code hello de ces procédures :

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Charger, évaluer et enregistrer les résultats de hello.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Output:**

ROC sur les données de test = 0,9827381497557599

Utilisation de Python sur la courbe de ROC Pandas données frames tooplot hello local.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


**Output:**

![Courbe ROC de remise de pourboire ou non](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Créer un modèle de classification par forêts aléatoires
Ensuite, créez un modèle de classification de forêt aléatoire à l’aide de hello Spark ML `RandomForestClassifier()` de fonction et pour évaluer le modèle hello sur les données de test.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Output:**

ROC sur les données de test = 0.9847103571552683

### <a name="create-a-gbt-classification-model"></a>Créer un modèle de classification GBT
Ensuite, créez un modèle de classification GBT à l’aide de MLlib `GradientBoostedTrees()` de fonction et pour évaluer le modèle hello sur les données de test.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Output:**

Zone sous courbe ROC = 0,9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Modèle de régression : prédire le montant du pourboire
Dans cette section, vous créez deux types de quantité de régression modèles toopredict hello Conseil :

* A **modèle de régression linéaire régularisée** à l’aide de hello Spark ML `LinearRegression()` (fonction). Vous allez enregistrer le modèle de hello et évaluer le modèle hello sur les données de test.
* A **renforcement de dégradé de modèle de régression arborescence** à l’aide de hello Spark ML `GBTRegressor()` (fonction).

### <a name="create-a-regularized-linear-regression-model"></a>Créer un modèle de régression linéaire régularisée
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cellule de temps toorun hello : 13 secondes.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Output:**

R-sqr sur les données de test = 0,5960320470835743

Requête suivante, hello des résultats des tests en tant qu’une trame de données et l’utiliser AutoVizWidget et matplotlib toovisualize il.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

code de Hello crée une trame de données local à partir de la sortie de la requête hello et trace les données de salutation. Hello `%%local` magique crée une trame de données locales, `sqlResults`, que vous pouvez utiliser tooplot avec matplotlib.

> [!NOTE]
> Cette commande magique Spark est utilisée plusieurs fois lors de cet article. Si la quantité de hello de données est importante, vous devez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.
> 
> 

Créez des tracés en utilisant matplotlib de Python.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Output:**

![Montant du pourboire : réel vs. prédit](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Créer un modèle de régression GBT
Créer un modèle de régression GBT à l’aide de hello Spark ML `GBTRegressor()` de fonction et pour évaluer le modèle hello sur les données de test.

[Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision. Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte. Vous pouvez utiliser les GBT pour la régression et la classification. Ils gèrent les caractéristiques catégorielles, ne requièrent aucune mise à l’échelle des caractéristiques et peuvent capturer les non-linéarités ainsi que les interactions entre les caractéristiques. Vous pouvez également les utiliser dans le paramétrage de classification multiclasse.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Output:**

Le R-sqr de test est : 0,7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>Utilitaires de modélisation avancée pour l’optimisation
Dans cette section, vous exécutez les utilitaires Machine Learning que les développeurs utilisent souvent pour l’optimisation du modèle. Plus précisément, vous pouvez optimiser les modèles Machine Learning de trois façons à l’aide du balayage paramétrique et de la validation croisée :

* Fractionner les données de hello en jeux d’apprentissage et de validation, optimiser le modèle de hello sur un jeu d’apprentissage à l’aide de balayage des paramètres hyper et évaluer sur un ensemble de validation (régression linéaire)
* Optimiser le modèle de hello à l’aide de la validation croisée et hyper-paramètre de balayage à l’aide CrossValidator fonction de Spark ML (classification binaire)
* Optimiser le modèle de hello à l’aide de code personnalisé de validation croisée et le balayage des paramètres toouse n’importe quel ensemble de la fonction et de paramètre (régression linéaire) d’apprentissage

**La validation croisée** est une technique qui évalue le degré un modèle formé sur un jeu connu de données généralise les fonctionnalités de hello toopredict des jeux de données sur lequel il n’a pas été effectué. Bonjour une idée générale de cette technique est qu’un modèle est formé sur un jeu de données de données connues et hello exactitude des prédictions est ensuite testé sur un jeu de données indépendant. Une implémentation courante est toodivide un jeu de données en *k*-prise en charge et puis effectuer l’apprentissage de modèle hello de façon alternée sur tous les mais l’un des plis de hello.

**Optimisation de Hyper-paramètre** problème hello de choisir un ensemble de paramètres hyper-pour un algorithme d’apprentissage, généralement avec comme objectif hello d’optimisation d’une mesure des performances de l’algorithme hello sur un jeu de données indépendant. Un paramètre-hyper est une valeur que vous devez spécifier en dehors de la procédure de formation de modèle hello. Hypothèses sur les valeurs de paramètre hyper peuvent affecter la flexibilité de hello et la précision du modèle de hello. Les arbres de décision ont hyper-paramètres, par exemple, telles que hello souhaité profondeur et nombre de feuilles dans l’arborescence de hello. Vous devez définir un terme de pénalité en cas d’erreur de classification pour une machine à vecteurs de support (SVM).

Une façon tooperform hyper-paramètre optimisation courante consiste toouse une recherche de la grille, également appelé un **balayage de paramètre**. Dans une recherche de la grille, une recherche exhaustive est effectuée par le biais d’un sous-ensemble spécifié de l’espace de hyper-paramètre hello pour un algorithme d’apprentissage, les valeurs hello. La validation croisée peut fournir un toosort de métriques de performances out produits par l’algorithme de recherche hello grille des résultats optimaux hello. Si vous utilisez le balayage des paramètres hyper validation croisée, vous pouvez aider les problèmes de limite le surajustement un tootraining de données de modèle. De cette manière, le modèle de hello conserve hello capacité tooapply toohello général jeu de données à partir de quels hello les données d’apprentissage ont été extraites.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Optimiser un modèle de régression linéaire avec le balayage paramétrique
Ensuite, fractionner les données en jeux d’apprentissage et de validation, utilisez hyper-balayage des paramètres sur une formation toooptimize hello modèle défini et évaluer sur un ensemble de validation (régression linéaire).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Output:**

Le R-sqr de test est : 0,6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Optimiser le modèle de classification binaire hello à l’aide de la validation croisée et hyper-paramètre de balayage
Cette section vous montre comment toooptimize une classification binaire modèle à l’aide de la validation croisée et hyper-paramètre de balayage. Cette méthode utilise hello Spark ML `CrossValidator` (fonction).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Output:**

Cellule de temps toorun hello : 33 secondes.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Optimiser le modèle de régression linéaire hello en utilisant le code de validation croisée et le balayage des paramètres personnalisé
Ensuite, optimiser le modèle de hello à l’aide de code personnalisé et identifier les meilleurs paramètres de modèle hello à l’aide de critère hello de précision la plus élevée. Ensuite, créez le modèle final de hello, évaluer le modèle hello sur les données de test et enregistrer le modèle de hello dans le stockage Blob. Enfin, charger le modèle de hello, évaluer les données de test et évaluer la précision.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Output:**

Cellule de temps toorun hello : 61 secondes.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Utiliser des modèles Machine Learning basés sur Spark générés automatiquement avec Scala
Pour une vue d’ensemble des rubriques qui vous guident tout au long des tâches de hello qui impliquent des processus de science des données hello dans Azure, consultez [processus de science des données équipe](http://aka.ms/datascienceprocess).

[Procédures pas à pas du processus de science des données de l’équipe](data-science-process-walkthroughs.md) décrit d’autres procédures pas à pas bout en bout qui illustrent les étapes hello Bonjour processus de science des données équipe pour des scénarios spécifiques. procédures pas à pas Hello également illustrent comment toocombine cloud et locaux outils et services dans un toocreate de flux de travail ou d’un pipeline, une application intelligente.

[Un score de modèles d’apprentissage intégré Spark](machine-learning-data-science-spark-model-consumption.md) vous montre comment toouse Scala code tooautomatically charger et évaluer les nouveaux jeux de données avec des modèles d’apprentissage intégré Spark et enregistrées dans le stockage d’objets Blob Azure. Vous pouvez de suivre les instructions hello fournies et remplacez simplement hello code Python avec le code Scala dans cet article pour la consommation automatique.

