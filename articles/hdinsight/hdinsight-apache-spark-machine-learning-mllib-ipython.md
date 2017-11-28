---
title: "exemple avec MLlib Spark sur HDInsight - Azure d’apprentissage d’aaaMachine | Documents Microsoft"
description: "Découvrez comment toouse Spark MLlib toocreate une application d’apprentissage machine qui analyse un dataset à l’aide de la classification de régression logistique."
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="81fe5-104">Utiliser Spark MLlib toobuild une application d’apprentissage et analyser un jeu de données</span><span class="sxs-lookup"><span data-stu-id="81fe5-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="81fe5-105">Découvrez comment toouse Spark **MLlib** toocreate une application toodo simple analyse prédictive sur Ouvrir un jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="81fe5-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="81fe5-106">À partir des bibliothèques de Machine Learning intégrées de Spark, cet exemple utilise une *classification* de régression logistique.</span><span class="sxs-lookup"><span data-stu-id="81fe5-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="81fe5-107">Ce exemple est également disponible en tant que bloc-notes Jupyter sur un cluster Spark (Linux) que vous créez dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81fe5-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="81fe5-108">expérience de bloc-notes Hello vous permet d’exécuter des extraits de code hello Python à partir de l’ordinateur portable hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="81fe5-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="81fe5-109">didacticiel de hello toofollow à partir d’un ordinateur portable, créer un Spark cluster et lancez un bloc-notes jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="81fe5-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="81fe5-110">Ensuite, exécutez bloc-notes de hello **Spark Machine Learning - analyse prédictive sur les données d’inspection de produits alimentaires à l’aide de MLlib.ipynb** sous hello **Python** dossier.</span><span class="sxs-lookup"><span data-stu-id="81fe5-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="81fe5-111">MLLib est une bibliothèque principale Spark qui fournit de nombreux utilitaires pratiques pour l’exécution de tâches de Machine Learning. Certains de ces utilitaires conviennent pour les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="81fe5-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="81fe5-112">Classification</span><span class="sxs-lookup"><span data-stu-id="81fe5-112">Classification</span></span>
* <span data-ttu-id="81fe5-113">Régression</span><span class="sxs-lookup"><span data-stu-id="81fe5-113">Regression</span></span>
* <span data-ttu-id="81fe5-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="81fe5-114">Clustering</span></span>
* <span data-ttu-id="81fe5-115">Modélisation de rubrique</span><span class="sxs-lookup"><span data-stu-id="81fe5-115">Topic modeling</span></span>
* <span data-ttu-id="81fe5-116">Décomposition de valeur singulière (SVD) et analyse des composants principaux (PCA)</span><span class="sxs-lookup"><span data-stu-id="81fe5-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="81fe5-117">Hypothèse de test et de calcul des exemples de statistiques</span><span class="sxs-lookup"><span data-stu-id="81fe5-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="81fe5-118">Qu’est-ce que la classification et la régression logistique ?</span><span class="sxs-lookup"><span data-stu-id="81fe5-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="81fe5-119">*Classification*, une tâche, d’apprentissage populaire est hello les processus de tri des données d’entrée en catégories.</span><span class="sxs-lookup"><span data-stu-id="81fe5-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="81fe5-120">Il s’agit de travail hello d’un toofigure d’algorithme de classification comment tooassign « étiquettes » tooinput les données que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="81fe5-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="81fe5-121">Par exemple, vous pourriez utiliser un algorithme d’apprentissage automatique qui accepte les informations de stock en tant qu’entrée et divise hello stock en deux catégories : que vous devez vendre et des stocks vous devez prendre.</span><span class="sxs-lookup"><span data-stu-id="81fe5-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="81fe5-122">La régression logistique est un algorithme de hello que vous utilisez pour la classification.</span><span class="sxs-lookup"><span data-stu-id="81fe5-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="81fe5-123">L’API de régression logistique de Spark est utile pour la *classification binaire*ou pour classer les données d’entrée dans un des deux groupes.</span><span class="sxs-lookup"><span data-stu-id="81fe5-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="81fe5-124">Pour plus d’informations sur la régression logistique, consultez [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="81fe5-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="81fe5-125">En résumé, le processus hello de régression logistique génère une *fonction logistique* qui peut être utilisé toopredict hello probabilité est qu’un vecteur d’entrée appartienne à un groupe ou hello autres.</span><span class="sxs-lookup"><span data-stu-id="81fe5-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="81fe5-126">Exemple d’analyse prédictive sur des données d’inspection alimentaire</span><span class="sxs-lookup"><span data-stu-id="81fe5-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="81fe5-127">Dans cet exemple, vous utilisez Spark tooperform des analyses prédictives sur les données d’inspection alimentaires (**Food_Inspections1.csv**) qui a été acquis via hello [portail de données Ville de Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="81fe5-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="81fe5-128">Ce jeu de données contient des informations sur les contrôles d’établissement alimentaires qui ont été effectués à Chicago, notamment des informations sur chacun d’eux, les violations de hello trouvée (le cas échéant) et hello les résultats de l’inspection de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="81fe5-129">fichier de données CSV Hello est déjà disponible dans hello compte de stockage associé au cluster hello à **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="81fe5-130">Dans la procédure hello ci-dessous, vous développez un modèle toosee à ce qu’il faut toopass ou échouer une inspection de produits alimentaires.</span><span class="sxs-lookup"><span data-stu-id="81fe5-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="81fe5-131">Commencer à créer une application de Machine Learning Spark MMLib</span><span class="sxs-lookup"><span data-stu-id="81fe5-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="81fe5-132">À partir de hello [portail Azure](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="81fe5-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="81fe5-133">Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="81fe5-134">Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="81fe5-135">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="81fe5-136">Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="81fe5-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="81fe5-137">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="81fe5-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="81fe5-138">Créez un bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="81fe5-138">Create a notebook.</span></span> <span data-ttu-id="81fe5-139">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="81fe5-140">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="81fe5-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="81fe5-141">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="81fe5-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="81fe5-142">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="81fe5-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="81fe5-143">![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "fournir un nom d’ordinateur portable de hello")</span><span class="sxs-lookup"><span data-stu-id="81fe5-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="81fe5-144">Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="81fe5-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="81fe5-145">contextes de Spark et Hive Hello sont créées automatiquement pour vous lors de l’exécution de la première cellule de code hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="81fe5-146">Vous pouvez commencer à créer votre application d’apprentissage en important les types hello requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="81fe5-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="81fe5-147">toodo, placez le curseur de hello dans la cellule de hello et appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="81fe5-148">Construire une trame de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="81fe5-148">Construct an input dataframe</span></span>
<span data-ttu-id="81fe5-149">Nous pouvons utiliser `sqlContext` tooperform des transformations sur des données structurées.</span><span class="sxs-lookup"><span data-stu-id="81fe5-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="81fe5-150">tâche première Hello est données d’exemple hello tooload ((**Food_Inspections1.csv**)) dans un Spark SQL *trame de données*.</span><span class="sxs-lookup"><span data-stu-id="81fe5-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="81fe5-151">Étant donné que les données brutes hello sont dans un format CSV, nous devons toouse hello Spark contexte toopull chaque ligne du fichier de hello en mémoire sous forme de texte non structuré ; Ensuite, vous utilisez tooparse de bibliothèque Python CSV chaque ligne individuellement.</span><span class="sxs-lookup"><span data-stu-id="81fe5-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="81fe5-152">Nous disposons désormais d’un fichier CSV hello comme un RDD.</span><span class="sxs-lookup"><span data-stu-id="81fe5-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="81fe5-153">schéma de hello toounderstand de données de hello, nous permet de récupérer une ligne à partir de hello RDD.</span><span class="sxs-lookup"><span data-stu-id="81fe5-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="81fe5-154">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="81fe5-155">Hello sortie précédente nous donne une idée du schéma hello du fichier d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="81fe5-156">Il inclut le nom hello de chaque établissement, le type hello de l’établissement, l’adresse de hello, données hello de contrôles de hello et l’emplacement de hello, entre autres choses.</span><span class="sxs-lookup"><span data-stu-id="81fe5-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="81fe5-157">Nous allons sélectionner plusieurs colonnes qui sont utiles pour notre analyse prédictive et regroupement les résultats de hello en tant qu’une trame de données, ce qui nous puis utilisent toocreate une table temporaire.</span><span class="sxs-lookup"><span data-stu-id="81fe5-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="81fe5-158">Nous avons maintenant un *tableau de données*, `df` sur lequel nous pouvons effectuer l’analyse.</span><span class="sxs-lookup"><span data-stu-id="81fe5-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="81fe5-159">Nous obtenons également une table temporaire **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="81fe5-160">Nous avons inclus des quatre colonnes dignes d’intérêt dans la trame de données hello : **id**, **nom**, **résultats**, et **violations**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="81fe5-161">Nous allons obtenir un petit échantillon de données de salutation :</span><span class="sxs-lookup"><span data-stu-id="81fe5-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="81fe5-162">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="81fe5-163">Comprendre les données de salutation</span><span class="sxs-lookup"><span data-stu-id="81fe5-163">Understand hello data</span></span>
1. <span data-ttu-id="81fe5-164">Nous pouvons commencer tooget une idée de ce que notre jeu de données contient.</span><span class="sxs-lookup"><span data-stu-id="81fe5-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="81fe5-165">Par exemple, quelles sont les valeurs différentes de hello Bonjour **résultats** colonne ?</span><span class="sxs-lookup"><span data-stu-id="81fe5-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="81fe5-166">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="81fe5-167">Une visualisation rapide peut nous aider à raison sur la distribution de hello de ces résultats.</span><span class="sxs-lookup"><span data-stu-id="81fe5-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="81fe5-168">Nous avons déjà les données de salutation dans une table temporaire **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="81fe5-169">Vous pouvez exécuter hello suivant la requête SQL sur hello table tooget une meilleure compréhension de la répartition des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="81fe5-170">Hello `%%sql` magique suivie `-o countResultsdf` garantit que sortie hello de requête de hello est rendu persistant localement sur le serveur de Notebook hello (généralement hello nœud principal du cluster de hello).</span><span class="sxs-lookup"><span data-stu-id="81fe5-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="81fe5-171">sortie de Hello est conservée en tant qu’un [Pandas](http://pandas.pydata.org/) nom spécifié de trame de données avec hello **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="81fe5-172">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="81fe5-173">![Résultat de la requête SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Résultat de la requête SQL")</span><span class="sxs-lookup"><span data-stu-id="81fe5-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="81fe5-174">Pour plus d’informations sur hello `%%sql` magique et autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="81fe5-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="81fe5-175">Vous pouvez également utiliser Matplotlib, une bibliothèque utilisée tooconstruct une visualisation des données, toocreate un tracé.</span><span class="sxs-lookup"><span data-stu-id="81fe5-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="81fe5-176">Étant donné que le traçage de hello doit être créé à partir de hello localement persistantes **countResultsdf** trame de données, l’extrait de code hello doit commencer par hello `%%local` magique.</span><span class="sxs-lookup"><span data-stu-id="81fe5-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="81fe5-177">Cela garantit que le code de hello est exécuté localement sur le serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="81fe5-178">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="81fe5-179">![Sortie de l’application de Machine Learning Spark : graphique en secteurs avec cinq résultats d’inspection distincts](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Sortie du résultat de l’application de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="81fe5-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="81fe5-180">Vous pouvez voir qu’il existe 5 résultats d’inspection distincts.</span><span class="sxs-lookup"><span data-stu-id="81fe5-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="81fe5-181">Entreprise introuvable</span><span class="sxs-lookup"><span data-stu-id="81fe5-181">Business not located</span></span>
   * <span data-ttu-id="81fe5-182">Échec</span><span class="sxs-lookup"><span data-stu-id="81fe5-182">Fail</span></span>
   * <span data-ttu-id="81fe5-183">Réussite</span><span class="sxs-lookup"><span data-stu-id="81fe5-183">Pass</span></span>
   * <span data-ttu-id="81fe5-184">Réussite avec conditions</span><span class="sxs-lookup"><span data-stu-id="81fe5-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="81fe5-185">Cessation d’activités</span><span class="sxs-lookup"><span data-stu-id="81fe5-185">Out of Business</span></span>

     <span data-ttu-id="81fe5-186">Nous développer un modèle qui peut deviner résultat hello d’une inspection de produits alimentaires, les violations de hello donné.</span><span class="sxs-lookup"><span data-stu-id="81fe5-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="81fe5-187">Étant donné que la régression logistique est une méthode de classification binaire, il est logique toogroup nos données en deux catégories : **échouer** et **passer**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="81fe5-188">Un « passer avec Conditions » est toujours un passage, donc lorsque nous former le modèle de hello, nous considérons hello deux résultats équivalent.</span><span class="sxs-lookup"><span data-stu-id="81fe5-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="81fe5-189">Données avec hello autres résultats (« Business introuvable » ou « d’entreprise ») ne sont pas utiles pour nous les supprimer à partir de notre jeu d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="81fe5-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="81fe5-190">Étant donné que ces deux catégories constituent un très petit pourcentage de résultats de hello tout de même, il doit être OK.</span><span class="sxs-lookup"><span data-stu-id="81fe5-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="81fe5-191">À présent, convertissons notre trame de données existante (`df`) en une nouvelle trame de données dans laquelle chaque inspection est représentée par une paire de violations étiquetée.</span><span class="sxs-lookup"><span data-stu-id="81fe5-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="81fe5-192">Dans notre cas, une étiquette `0.0` représente un échec, une étiquette `1.0` représente une réussite et une étiquette `-1.0` représente d’autres résultats.</span><span class="sxs-lookup"><span data-stu-id="81fe5-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="81fe5-193">Nous filtrer ces autres résultats lors du calcul de nouvelle trame de données hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="81fe5-194">toosee quel hello étiqueté ressemble à des données, nous allons extraire une ligne.</span><span class="sxs-lookup"><span data-stu-id="81fe5-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="81fe5-195">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="81fe5-196">Créer un modèle de régression logistique à partir de la trame de données d’entrée hello</span><span class="sxs-lookup"><span data-stu-id="81fe5-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="81fe5-197">La dernière tâche est hello tooconvert intitulé des données dans un format qui peut être analysé par la régression logistique.</span><span class="sxs-lookup"><span data-stu-id="81fe5-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="81fe5-198">algorithme de régression logistique Hello tooa d’entrée doit être un ensemble de *paires de vecteur de fonctionnalité d’étiquettes*, où hello « vecteur de fonctionnalité » est un vecteur de nombres représentant le point d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="81fe5-199">Par conséquent, nous devons colonne tooconvert des violations « hello », qui est semi-structurées et contient le nombre de commentaires dans le tableau de tooan en texte libre, de nombres réels qui comprend un ordinateur facilement.</span><span class="sxs-lookup"><span data-stu-id="81fe5-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="81fe5-200">Une approche d’apprentissage machine standard pour le traitement en langage naturel est tooassign chaque mot distinct un « index » et transmettez un vecteur toohello algorithme d’apprentissage tels que les valeur de chaque index contient la fréquence relative de hello de ce mot dans le texte hello chaîne.</span><span class="sxs-lookup"><span data-stu-id="81fe5-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="81fe5-201">MLlib fournit un moyen simple de tooperform cette opération.</span><span class="sxs-lookup"><span data-stu-id="81fe5-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="81fe5-202">Tout d’abord, « réinitialiser » chaque violations chaîne tooget hello mots individuels dans chaque chaîne.</span><span class="sxs-lookup"><span data-stu-id="81fe5-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="81fe5-203">Ensuite, utilisez un `HashingTF` tooconvert chaque ensemble de jetons dans un vecteur de fonctionnalité qui peut ensuite être tooconstruct d’algorithme de régression logistique toohello passé un modèle.</span><span class="sxs-lookup"><span data-stu-id="81fe5-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="81fe5-204">Nous allons effectuer toutes ces étapes successivement à l’aide d’un « pipeline ».</span><span class="sxs-lookup"><span data-stu-id="81fe5-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="81fe5-205">Évaluation du modèle hello sur un jeu de données de test distinct</span><span class="sxs-lookup"><span data-stu-id="81fe5-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="81fe5-206">Nous pouvons utiliser le modèle hello créée précédemment trop*prédire* quel hello résultats de nouveaux contrôles sera, en fonction de violations hello qui ont été observées.</span><span class="sxs-lookup"><span data-stu-id="81fe5-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="81fe5-207">Nous ce modèle entraîné sur hello dataset **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="81fe5-208">Nous utiliser un deuxième dataset **Food_Inspections2.csv**, trop*évaluer* hello puissance de ce modèle sur de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="81fe5-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="81fe5-209">Ce deuxième ensemble de données (**Food_Inspections2.csv**) doit être déjà dans le conteneur de stockage par défaut hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="81fe5-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="81fe5-210">Hello extrait de code suivant crée une nouvelle trame de données, **predictionsDf** qui contient la prédiction hello générée par le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="81fe5-211">extrait de code Hello crée également une table temporaire nommée **prédictions** en fonction de la trame de données hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="81fe5-212">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="81fe5-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="81fe5-213">Recherchez une des prédictions de hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-213">Look at one of hello predictions.</span></span> <span data-ttu-id="81fe5-214">Exécutez cet extrait de code :</span><span class="sxs-lookup"><span data-stu-id="81fe5-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="81fe5-215">Il existe une prédiction pour hello première entrée de jeu de données de test hello.</span><span class="sxs-lookup"><span data-stu-id="81fe5-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="81fe5-216">Hello `model.transform()` méthode s’applique hello même transformation tooany nouvelles données avec hello même schéma et arrivent à une prédiction de comment tooclassify hello des données.</span><span class="sxs-lookup"><span data-stu-id="81fe5-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="81fe5-217">Nous pouvons effectuer certains tooget statistiques simple une idée de la précision de nos prédictions étaient :</span><span class="sxs-lookup"><span data-stu-id="81fe5-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="81fe5-218">sortie de Hello ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="81fe5-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="81fe5-219">À l’aide de la régression logistique avec Spark nous donne un modèle précis de relation hello entre des descriptions de violations en anglais et indique si une activité donnée est réussir ou d’échouer une inspection de produits alimentaires.</span><span class="sxs-lookup"><span data-stu-id="81fe5-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="81fe5-220">Créer une représentation visuelle de prédiction de hello</span><span class="sxs-lookup"><span data-stu-id="81fe5-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="81fe5-221">Nous pouvons maintenant construire un toohelp visualisation final que nous analyser les résultats de hello de ce test.</span><span class="sxs-lookup"><span data-stu-id="81fe5-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="81fe5-222">Nous allons commencer en extrayant des prédictions différentes hello et résultats de hello **prédictions** table temporaire créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="81fe5-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="81fe5-223">Hello de requêtes suivants hello une sortie distincte en tant que *true_positive*, *false_positive*, *true_negative*, et *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="81fe5-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="81fe5-224">Dans les requêtes de hello ci-dessous, nous désactivons visualisation à l’aide de `-q` et également enregistrer la sortie de hello (à l’aide de `-o`) en tant que les trames de données qui peuvent être utilisées ensuite par hello `%%local` magique.</span><span class="sxs-lookup"><span data-stu-id="81fe5-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="81fe5-225">Enfin, utilisez hello suivant à l’aide d’extrait toogenerate hello traçage **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="81fe5-226">Vous devez voir hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="81fe5-226">You should see hello following output:</span></span>

    <span data-ttu-id="81fe5-227">![Sortie de l’application de Machine Learning Spark : graphique en secteurs des pourcentages d’inspections alimentaires qui ont échoué.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Sortie du résultat de l’application de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="81fe5-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="81fe5-228">Dans ce graphique, un résultat « positif » fait référence toohello échoué de l’inspection de produits alimentaires, tandis qu’un résultat négatif tooa passé inspection.</span><span class="sxs-lookup"><span data-stu-id="81fe5-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="81fe5-229">Arrêter le bloc-notes de hello</span><span class="sxs-lookup"><span data-stu-id="81fe5-229">Shut down hello notebook</span></span>
<span data-ttu-id="81fe5-230">Une fois que vous avez terminé d’exécuter l’application hello, vous devez arrêter les ressources de hello toorelease hello bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="81fe5-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="81fe5-231">toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.</span><span class="sxs-lookup"><span data-stu-id="81fe5-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="81fe5-232">Cette opération arrête et ferme hello bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="81fe5-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="81fe5-233"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="81fe5-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="81fe5-234">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="81fe5-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="81fe5-235">Scénarios</span><span class="sxs-lookup"><span data-stu-id="81fe5-235">Scenarios</span></span>
* [<span data-ttu-id="81fe5-236">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="81fe5-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="81fe5-237">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="81fe5-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="81fe5-238">Streaming Spark : utilisez Spark dans HDInsight pour créer des applications de streaming en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="81fe5-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="81fe5-239">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="81fe5-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="81fe5-240">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="81fe5-240">Create and run applications</span></span>
* [<span data-ttu-id="81fe5-241">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="81fe5-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="81fe5-242">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="81fe5-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="81fe5-243">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="81fe5-243">Tools and extensions</span></span>
* [<span data-ttu-id="81fe5-244">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="81fe5-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="81fe5-245">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="81fe5-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="81fe5-246">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="81fe5-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="81fe5-247">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="81fe5-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="81fe5-248">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="81fe5-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="81fe5-249">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="81fe5-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="81fe5-250">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="81fe5-250">Manage resources</span></span>
* [<span data-ttu-id="81fe5-251">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="81fe5-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="81fe5-252">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="81fe5-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
