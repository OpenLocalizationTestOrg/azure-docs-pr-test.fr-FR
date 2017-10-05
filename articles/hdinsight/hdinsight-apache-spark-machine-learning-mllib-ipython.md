---
title: Exemple de Machine Learning avec Spark MLlib sur HDInsight - Azure | Microsoft Docs
description: "Découvrez comment utiliser Spark MLlib pour créer une application de Machine Learning qui analyse un jeu de données à l’aide d’une classification de régression logistique."
keywords: machine learning spark, exemple de machine learning spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="8f99c-104">Utiliser Spark MLlib pour créer une application de Machine Learning et analyser un jeu de données</span><span class="sxs-lookup"><span data-stu-id="8f99c-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="8f99c-105">Découvrez comment utiliser Spark **MLlib** pour créer une application de Machine Learning afin d’effectuer une analyse prédictive simple sur un jeu de données ouvert.</span><span class="sxs-lookup"><span data-stu-id="8f99c-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="8f99c-106">À partir des bibliothèques de Machine Learning intégrées de Spark, cet exemple utilise une *classification* de régression logistique.</span><span class="sxs-lookup"><span data-stu-id="8f99c-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="8f99c-107">Ce exemple est également disponible en tant que bloc-notes Jupyter sur un cluster Spark (Linux) que vous créez dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8f99c-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="8f99c-108">L’interface du bloc-notes vous permet d’exécuter des extraits de code Python à partir du bloc-notes lui-même.</span><span class="sxs-lookup"><span data-stu-id="8f99c-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="8f99c-109">Pour suivre le didacticiel à partir d’un bloc-notes, créez un cluster Spark et lancez un bloc-notes Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="8f99c-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="8f99c-110">Ensuite, exécutez le bloc-notes, **Machine Learning Spark : analyse prédictive des données d’inspections alimentaires à l’aide de MLLib** figurant dans le dossier **Python**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="8f99c-111">MLLib est une bibliothèque principale Spark qui fournit de nombreux utilitaires pratiques pour l’exécution de tâches de Machine Learning. Certains de ces utilitaires conviennent pour les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="8f99c-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="8f99c-112">Classification</span><span class="sxs-lookup"><span data-stu-id="8f99c-112">Classification</span></span>
* <span data-ttu-id="8f99c-113">Régression</span><span class="sxs-lookup"><span data-stu-id="8f99c-113">Regression</span></span>
* <span data-ttu-id="8f99c-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="8f99c-114">Clustering</span></span>
* <span data-ttu-id="8f99c-115">Modélisation de rubrique</span><span class="sxs-lookup"><span data-stu-id="8f99c-115">Topic modeling</span></span>
* <span data-ttu-id="8f99c-116">Décomposition de valeur singulière (SVD) et analyse des composants principaux (PCA)</span><span class="sxs-lookup"><span data-stu-id="8f99c-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="8f99c-117">Hypothèse de test et de calcul des exemples de statistiques</span><span class="sxs-lookup"><span data-stu-id="8f99c-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="8f99c-118">Qu’est-ce que la classification et la régression logistique ?</span><span class="sxs-lookup"><span data-stu-id="8f99c-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="8f99c-119">Une *classification*, tâche de Machine Learning très courante, est le processus de tri de données d’entrée par catégories.</span><span class="sxs-lookup"><span data-stu-id="8f99c-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="8f99c-120">L’algorithme de classification doit déterminer comment attribuer les « étiquettes » aux données d’entrée que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="8f99c-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="8f99c-121">Par exemple, vous pouvez utiliser un algorithme Machine Learning qui accepte les informations de stock en tant qu’entrée et divise le stock en deux catégories : ce qu’il faut vendre et ce qu’il faut conserver.</span><span class="sxs-lookup"><span data-stu-id="8f99c-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="8f99c-122">La régression logistique correspond à l’algorithme que vous utilisez pour la classification.</span><span class="sxs-lookup"><span data-stu-id="8f99c-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="8f99c-123">L’API de régression logistique de Spark est utile pour la *classification binaire*ou pour classer les données d’entrée dans un des deux groupes.</span><span class="sxs-lookup"><span data-stu-id="8f99c-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="8f99c-124">Pour plus d’informations sur la régression logistique, consultez [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="8f99c-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="8f99c-125">En résumé, le processus de régression logistique génère une *fonction logistique* qui peut être utilisée pour prédire la probabilité qu’un vecteur d’entrée appartienne à un groupe ou à l’autre.</span><span class="sxs-lookup"><span data-stu-id="8f99c-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="8f99c-126">Exemple d’analyse prédictive sur des données d’inspection alimentaire</span><span class="sxs-lookup"><span data-stu-id="8f99c-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="8f99c-127">Dans cet exemple, vous utilisez Spark pour effectuer une analyse prédictive de données d’inspection alimentaire (**Food_Inspections1.csv**) qui ont été acquises via le [portail de données de la ville de Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="8f99c-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="8f99c-128">Ce jeu de données contient des informations relatives aux inspections d’établissements alimentaires effectuées à Chicago, notamment des informations sur chaque établissement, les violations éventuelles relevées et les résultats des inspections.</span><span class="sxs-lookup"><span data-stu-id="8f99c-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="8f99c-129">Le fichier de données CSV est déjà disponible dans le compte de stockage associé au cluster dans **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="8f99c-130">Dans la procédure ci-dessous, vous développez un modèle pour voir ce qui est nécessaire à la réussite ou à l’échec d’une inspection de produits alimentaires.</span><span class="sxs-lookup"><span data-stu-id="8f99c-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="8f99c-131">Commencer à créer une application de Machine Learning Spark MMLib</span><span class="sxs-lookup"><span data-stu-id="8f99c-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="8f99c-132">Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="8f99c-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="8f99c-133">Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="8f99c-134">Dans le panneau du cluster Spark, cliquez sur **Tableau de bord du cluster**, puis sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="8f99c-135">Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="8f99c-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f99c-136">Vous pouvez également atteindre le bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8f99c-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="8f99c-137">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="8f99c-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="8f99c-138">Créez un bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="8f99c-138">Create a notebook.</span></span> <span data-ttu-id="8f99c-139">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="8f99c-140">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="8f99c-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="8f99c-141">Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="8f99c-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="8f99c-142">Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="8f99c-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="8f99c-143">![Donnez un nom au bloc-notes](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Donnez un nom au bloc-notes")</span><span class="sxs-lookup"><span data-stu-id="8f99c-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="8f99c-144">Comme vous avez créé un bloc-notes à l’aide du noyau PySpark, il est inutile de créer des contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="8f99c-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="8f99c-145">Les contextes Spark et Hive sont automatiquement créés pour vous lorsque vous exécutez la première cellule de code.</span><span class="sxs-lookup"><span data-stu-id="8f99c-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="8f99c-146">Vous pouvez commencer à créer votre application d'apprentissage automatique en important les types requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="8f99c-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="8f99c-147">Pour ce faire, placez le curseur dans la cellule, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="8f99c-148">Construire une trame de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="8f99c-148">Construct an input dataframe</span></span>
<span data-ttu-id="8f99c-149">Nous pouvons utiliser `sqlContext` pour effectuer des transformations sur des données structurées.</span><span class="sxs-lookup"><span data-stu-id="8f99c-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="8f99c-150">La première tâche consiste à charger les exemples de données ((**Food_Inspections1.csv**)) dans un *tableau de données* SQL Spark.</span><span class="sxs-lookup"><span data-stu-id="8f99c-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="8f99c-151">Étant donné que les données brutes sont au format CSV, nous devons utiliser le contexte Spark pour extraire chaque ligne du fichier en mémoire sous forme de texte non structuré. Ensuite, utilisez la bibliothèque CSV de Python pour analyser chaque ligne individuellement.</span><span class="sxs-lookup"><span data-stu-id="8f99c-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="8f99c-152">Nous avons maintenant le fichier CSV sous forme de RDD.</span><span class="sxs-lookup"><span data-stu-id="8f99c-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="8f99c-153">Pour comprendre le schéma de données, nous extrayons une ligne du RDD.</span><span class="sxs-lookup"><span data-stu-id="8f99c-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="8f99c-154">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="8f99c-155">La sortie précédente donne une idée du schéma du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8f99c-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="8f99c-156">Elle inclut notamment, pour chaque établissement, le nom, le type, l’adresse, les données des inspections et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="8f99c-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="8f99c-157">Nous allons sélectionner quelques colonnes utiles pour notre analyse prédictive et regrouper les résultats dans une tramedonnées que nous utiliserons ensuite pour créer une table temporaire.</span><span class="sxs-lookup"><span data-stu-id="8f99c-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="8f99c-158">Nous avons maintenant un *tableau de données*, `df` sur lequel nous pouvons effectuer l’analyse.</span><span class="sxs-lookup"><span data-stu-id="8f99c-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="8f99c-159">Nous obtenons également une table temporaire **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="8f99c-160">Nous avons inclus dans la tramedonnées quatre colonnes intéressantes : **id**, **nom**, **résultats** et **violations**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="8f99c-161">Prenons un petit échantillon de données :</span><span class="sxs-lookup"><span data-stu-id="8f99c-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="8f99c-162">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="8f99c-163">Comprendre les données</span><span class="sxs-lookup"><span data-stu-id="8f99c-163">Understand the data</span></span>
1. <span data-ttu-id="8f99c-164">Commençons par nous faire une idée de ce que notre jeu de données contient.</span><span class="sxs-lookup"><span data-stu-id="8f99c-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="8f99c-165">Par exemple, quelles sont les différentes valeurs dans la colonne **résultats** ?</span><span class="sxs-lookup"><span data-stu-id="8f99c-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="8f99c-166">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="8f99c-167">Un aperçu rapide peut nous aider à examiner la distribution de ces résultats.</span><span class="sxs-lookup"><span data-stu-id="8f99c-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="8f99c-168">Nous avons déjà les données dans une table temporaire **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="8f99c-169">Vous pouvez exécuter la requête SQL suivante sur la table pour mieux comprendre la façon dont les résultats sont distribués.</span><span class="sxs-lookup"><span data-stu-id="8f99c-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="8f99c-170">La méthode `%%sql` suivie par `-o countResultsdf` garantit que le résultat de la requête est conservé localement sur le serveur Jupyter (généralement le nœud principal du cluster).</span><span class="sxs-lookup"><span data-stu-id="8f99c-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="8f99c-171">Le résultat est conservé sous la forme d’une trame de données [Pandas](http://pandas.pydata.org/) avec le nom spécifié **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="8f99c-172">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-172">You should see an output like the following:</span></span>

    <span data-ttu-id="8f99c-173">![Résultat de la requête SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Résultat de la requête SQL")</span><span class="sxs-lookup"><span data-stu-id="8f99c-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="8f99c-174">Pour plus d’informations sur la méthode magique `%%sql` et d’autres méthodes magiques disponibles avec le noyau PySpark, consultez [Noyaux disponibles sur les blocs-notes Jupyter avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="8f99c-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="8f99c-175">Vous pouvez également utiliser Matplotlib, une bibliothèque permettant de construire une visualisation des données, pour créer un tracé.</span><span class="sxs-lookup"><span data-stu-id="8f99c-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="8f99c-176">Étant donné que le tracé doit être créé à partir du tableau de données **countResultsdf** conservé localement, l’extrait de code doit commencer par la commande magique `%%local`.</span><span class="sxs-lookup"><span data-stu-id="8f99c-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="8f99c-177">Cela garantit l’exécution locale du code sur le serveur Jupyter.</span><span class="sxs-lookup"><span data-stu-id="8f99c-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="8f99c-178">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-178">You should see an output like the following:</span></span>

    <span data-ttu-id="8f99c-179">![Sortie de l’application de Machine Learning Spark : graphique en secteurs avec cinq résultats d’inspection distincts](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Sortie du résultat de l’application de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="8f99c-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="8f99c-180">Vous pouvez voir qu’il existe 5 résultats d’inspection distincts.</span><span class="sxs-lookup"><span data-stu-id="8f99c-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="8f99c-181">Entreprise introuvable</span><span class="sxs-lookup"><span data-stu-id="8f99c-181">Business not located</span></span>
   * <span data-ttu-id="8f99c-182">Échec</span><span class="sxs-lookup"><span data-stu-id="8f99c-182">Fail</span></span>
   * <span data-ttu-id="8f99c-183">Réussite</span><span class="sxs-lookup"><span data-stu-id="8f99c-183">Pass</span></span>
   * <span data-ttu-id="8f99c-184">Réussite avec conditions</span><span class="sxs-lookup"><span data-stu-id="8f99c-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="8f99c-185">Cessation d’activités</span><span class="sxs-lookup"><span data-stu-id="8f99c-185">Out of Business</span></span>

     <span data-ttu-id="8f99c-186">Développons un modèle capable de deviner le résultat d’une inspection alimentaire, en fonction des violations.</span><span class="sxs-lookup"><span data-stu-id="8f99c-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="8f99c-187">Étant donné que la régression logistique est une méthode de classification binaire, il est judicieux de regrouper les données en deux catégories : **échec** et **réussite**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="8f99c-188">Une « Réussite avec conditions » reste une Réussite. Par conséquent, lorsque nous formons le modèle, nous considérons ces deux résultats comme équivalents.</span><span class="sxs-lookup"><span data-stu-id="8f99c-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="8f99c-189">Les données contenant les autres résultats (« Entreprise introuvable » ou « Cessation d’activités ») étant inutiles, nous pouvons donc les supprimer de notre jeu d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="8f99c-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="8f99c-190">Cela ne devrait pas poser de problème, puisque ces deux catégories ne représentent qu’un faible pourcentage du résultat total.</span><span class="sxs-lookup"><span data-stu-id="8f99c-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="8f99c-191">À présent, convertissons notre trame de données existante (`df`) en une nouvelle trame de données dans laquelle chaque inspection est représentée par une paire de violations étiquetée.</span><span class="sxs-lookup"><span data-stu-id="8f99c-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="8f99c-192">Dans notre cas, une étiquette `0.0` représente un échec, une étiquette `1.0` représente une réussite et une étiquette `-1.0` représente d’autres résultats.</span><span class="sxs-lookup"><span data-stu-id="8f99c-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="8f99c-193">Nous filtrons ces autres résultats lors du calcul de la nouvelle trame de données.</span><span class="sxs-lookup"><span data-stu-id="8f99c-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="8f99c-194">Pour voir à quoi ressemblent les données étiquetées, extrayons une ligne.</span><span class="sxs-lookup"><span data-stu-id="8f99c-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="8f99c-195">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="8f99c-196">Créer un modèle de régression logistique à partir de la trame de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="8f99c-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="8f99c-197">La dernière tâche consiste à convertir les données étiquetées dans un format qui peut être analysé par régression logistique.</span><span class="sxs-lookup"><span data-stu-id="8f99c-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="8f99c-198">L’entrée dans un algorithme de régression logistique doit être un jeu de *paires de vecteurs étiquette-fonctionnalité*, où le « vecteur fonctionnalité » est un vecteur de nombres représentant le point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8f99c-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="8f99c-199">Nous devons donc convertir la colonne « violations », qui est semi-structurée et contient un grand nombre de commentaires sous forme de texte libre, en un tableau de nombres réels qu’une machine peut facilement comprendre.</span><span class="sxs-lookup"><span data-stu-id="8f99c-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="8f99c-200">Une approche Machine Learning standard pour le traitement du langage naturel consiste à assigner un « index » à chaque mot distinct et à transmettre un vecteur à l’algorithme de Machine Learning, de manière à ce que la valeur de chaque index contienne la fréquence relative de ce mot dans la chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="8f99c-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="8f99c-201">MLLib permet d’effectuer cette opération en toute simplicité.</span><span class="sxs-lookup"><span data-stu-id="8f99c-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="8f99c-202">Tout d’abord, il convertit en jetons chaque chaîne de violations afin d’obtenir les mots de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="8f99c-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="8f99c-203">Ensuite, il utilise un `HashingTF` pour convertir chaque ensemble de jetons en un vecteur fonctionnalité qui peut ensuite être transmis à l’algorithme de régression logistique pour construire un modèle.</span><span class="sxs-lookup"><span data-stu-id="8f99c-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="8f99c-204">Nous allons effectuer toutes ces étapes successivement à l’aide d’un « pipeline ».</span><span class="sxs-lookup"><span data-stu-id="8f99c-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="8f99c-205">Évaluer le modèle sur un jeu de données de test séparé</span><span class="sxs-lookup"><span data-stu-id="8f99c-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="8f99c-206">Nous pouvons utiliser le modèle que nous avons créé précédemment pour *prédire* les résultats des nouvelles inspections, en fonction des violations qui ont été observées.</span><span class="sxs-lookup"><span data-stu-id="8f99c-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="8f99c-207">Nous avons formé ce modèle sur le jeu de données **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="8f99c-208">Utilisons un second jeu de données, **Food_Inspections2.csv**, pour *évaluer* la puissance de ce modèle sur les nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="8f99c-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="8f99c-209">Ce second jeu de données (**Food_Inspections2.csv**) doit déjà se trouver dans le conteneur de stockage par défaut associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="8f99c-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="8f99c-210">L’extrait de code ci-dessous crée une tramedonnées, **predictionsDf**, qui contient la prédiction générée par le modèle.</span><span class="sxs-lookup"><span data-stu-id="8f99c-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="8f99c-211">Il crée également une table temporaire, **Predictions**, basée sur la tramedonnées.</span><span class="sxs-lookup"><span data-stu-id="8f99c-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="8f99c-212">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="8f99c-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="8f99c-213">Observez une des prédictions.</span><span class="sxs-lookup"><span data-stu-id="8f99c-213">Look at one of the predictions.</span></span> <span data-ttu-id="8f99c-214">Exécutez cet extrait de code :</span><span class="sxs-lookup"><span data-stu-id="8f99c-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="8f99c-215">Une prédiction pour la première entrée figure dans le jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="8f99c-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="8f99c-216">La méthode `model.transform()` applique la même transformation à toutes les nouvelles données possédant le même schéma afin d’obtenir une prédiction permettant de classer les données.</span><span class="sxs-lookup"><span data-stu-id="8f99c-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="8f99c-217">Nous pouvons faire des statistiques simples pour avoir une idée de la précision de nos prédictions :</span><span class="sxs-lookup"><span data-stu-id="8f99c-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="8f99c-218">La sortie a l'aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="8f99c-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="8f99c-219">À l’aide de la régression logistique, Spark fournit un modèle précis de la relation entre les descriptions des violations en anglais et indique si une entreprise donnée échoue ou réussit l’inspection alimentaire.</span><span class="sxs-lookup"><span data-stu-id="8f99c-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="8f99c-220">Créer une représentation visuelle de la prédiction</span><span class="sxs-lookup"><span data-stu-id="8f99c-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="8f99c-221">Nous pouvons désormais créer une visualisation finale pour nous aider à examiner les résultats de ce test.</span><span class="sxs-lookup"><span data-stu-id="8f99c-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="8f99c-222">Nous allons commencer par extraire les différentes prédictions et résultats de la table temporaire **Predictions** créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="8f99c-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="8f99c-223">Les requêtes suivantes séparent la sortie en tant que *true_positive*, *false_positive*, *true_negative* et *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="8f99c-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="8f99c-224">Dans les requêtes ci-dessous, nous désactivons la visualisation à l’aide de `-q` et nous enregistrons la sortie (à l’aide de `-o`) en tant que trames de données qui peuvent ensuite être utilisées avec la magie `%%local`.</span><span class="sxs-lookup"><span data-stu-id="8f99c-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="8f99c-225">Enfin, utilisez l’extrait suivant pour générer le tracé à l’aide de **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="8f99c-226">Vous devez normalement voir la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="8f99c-226">You should see the following output:</span></span>

    <span data-ttu-id="8f99c-227">![Sortie de l’application de Machine Learning Spark : graphique en secteurs des pourcentages d’inspections alimentaires qui ont échoué.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Sortie du résultat de l’application de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="8f99c-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="8f99c-228">Dans ce graphique, un résultat « positif » fait référence à l’inspection de produits alimentaires ayant échoué, tandis qu’un résultat négatif fait référence à une inspection réussie.</span><span class="sxs-lookup"><span data-stu-id="8f99c-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="8f99c-229">Arrêtez le bloc-notes</span><span class="sxs-lookup"><span data-stu-id="8f99c-229">Shut down the notebook</span></span>
<span data-ttu-id="8f99c-230">Une fois l’exécution de l’application terminée, fermez le bloc-notes pour libérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="8f99c-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="8f99c-231">Pour ce faire, dans le menu **Fichier** du bloc-notes, cliquez sur **Fermer et arrêter**.</span><span class="sxs-lookup"><span data-stu-id="8f99c-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="8f99c-232">Cela a pour effet d’arrêter et de fermer le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="8f99c-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="8f99c-233"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8f99c-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8f99c-234">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f99c-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8f99c-235">Scénarios</span><span class="sxs-lookup"><span data-stu-id="8f99c-235">Scenarios</span></span>
* [<span data-ttu-id="8f99c-236">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="8f99c-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8f99c-237">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="8f99c-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8f99c-238">Streaming Spark : utilisez Spark dans HDInsight pour créer des applications de streaming en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="8f99c-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8f99c-239">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f99c-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8f99c-240">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="8f99c-240">Create and run applications</span></span>
* [<span data-ttu-id="8f99c-241">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="8f99c-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8f99c-242">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="8f99c-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8f99c-243">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="8f99c-243">Tools and extensions</span></span>
* [<span data-ttu-id="8f99c-244">Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="8f99c-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8f99c-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="8f99c-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8f99c-246">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f99c-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8f99c-247">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f99c-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8f99c-248">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="8f99c-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8f99c-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8f99c-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8f99c-250">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="8f99c-250">Manage resources</span></span>
* [<span data-ttu-id="8f99c-251">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f99c-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8f99c-252">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f99c-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
