---
title: applications sur Azure HDInsight apprentissage Apache Spark automatique aaaBuild | Documents Microsoft
description: "Instructions détaillées sur la façon dont les clusters toobuild Apache Spark d’apprentissage application sur HDInsight Spark à l’aide du bloc-notes jupyter"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="ded7c-103">Créer des applications de Machine Learning Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="ded7c-104">Découvrez comment toobuild une application d’apprentissage machine Apache Spark à l’aide d’un Spark de cluster sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ded7c-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="ded7c-105">Cet article explique comment toouse hello bloc-notes jupyter disponible avec hello cluster toobuild et tester cette application.</span><span class="sxs-lookup"><span data-stu-id="ded7c-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="ded7c-106">application Hello utilise hello HVAC.csv d’un échantillon de données disponibles sur tous les clusters par défaut.</span><span class="sxs-lookup"><span data-stu-id="ded7c-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="ded7c-107">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="ded7c-107">**Prerequisites:**</span></span>

<span data-ttu-id="ded7c-108">Vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="ded7c-108">You must have hello following:</span></span>

* <span data-ttu-id="ded7c-109">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ded7c-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ded7c-110">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ded7c-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="ded7c-111"><a name="data"></a>Comprendre le jeu de données hello</span><span class="sxs-lookup"><span data-stu-id="ded7c-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="ded7c-112">Avant de commencer à générer l’application hello, faites-nous comprendre hello structure de données hello pour lequel nous générer application hello et type hello d’analyse, que nous ferons sur les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="ded7c-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="ded7c-113">Dans cet article, nous utilisons l’exemple hello **HVAC.csv** fichier de données qui est disponible dans hello compte de stockage Azure que vous avez associé le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="ded7c-114">Dans le compte de stockage hello, fichier de hello est à **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="ded7c-115">Téléchargez et ouvrez tooget de fichier CSV hello un instantané des données de hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="ded7c-116">![Capture instantanée des données utilisées pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Capture instantanée des données utilisées pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="ded7c-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="ded7c-117">les données de salutation montrent la température de cible de hello et hello de température réelle d’une construction qui HVAC système est installé.</span><span class="sxs-lookup"><span data-stu-id="ded7c-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="ded7c-118">Supposons que hello **système** colonne représente l’ID de système hello et hello **SystemAge** colonne représente le nombre de hello d’années système de climatisation hello a été mises en place au niveau de la construction de hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="ded7c-119">Si une génération sera chaudes ou surgelé basé sur la température de cible hello, étant donné un ID système et l’âge du système, nous utilisons cette toopredict de données.</span><span class="sxs-lookup"><span data-stu-id="ded7c-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="ded7c-120"><a name="app"></a>Écrire une application de Machine Learning Spark à l’aide de Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="ded7c-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="ded7c-121">Dans cette application, nous utilisons un tooperform de pipeline Spark ML une classification de document.</span><span class="sxs-lookup"><span data-stu-id="ded7c-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="ded7c-122">Dans le pipeline de hello, nous fractionner les documents de hello en mots, convertir les mots hello dans un vecteur de fonctionnalité numériques et enfin créer un modèle de prévision à l’aide d’étiquettes et les vecteurs de caractéristiques hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="ded7c-123">Effectuer hello après application de hello toocreate étapes.</span><span class="sxs-lookup"><span data-stu-id="ded7c-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="ded7c-124">À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="ded7c-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="ded7c-125">Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="ded7c-126">Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="ded7c-127">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ded7c-128">Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="ded7c-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="ded7c-129">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="ded7c-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="ded7c-130">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="ded7c-130">Create a new notebook.</span></span> <span data-ttu-id="ded7c-131">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="ded7c-132">![Créer un bloc-notes Jupyter pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Créer un bloc-notes Jupyter pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="ded7c-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="ded7c-133">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="ded7c-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="ded7c-134">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="ded7c-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="ded7c-135">![Fournir un nom de bloc-notes pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fournir un nom de bloc-notes pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="ded7c-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="ded7c-136">Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="ded7c-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="ded7c-137">contextes de Spark et Hive Hello seront automatiquement créés pour vous lors de l’exécution de la première cellule de code hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="ded7c-138">Vous pouvez commencer par importer les types hello qui sont requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="ded7c-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="ded7c-139">Collez hello suivant extrait dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="ded7c-140">Maintenant, vous devez charger les données de salutation (hvac.csv), analyser et utiliser le modèle de hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="ded7c-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="ded7c-141">Pour ce faire, vous définissez une fonction qui vérifie si la température réelle de hello de construction de hello est supérieure à la température de cible hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="ded7c-142">Si la température réelle de hello est supérieure, génération de hello est à chaud, représentée par la valeur de hello **1.0**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="ded7c-143">Si la température réelle de hello est moindre, génération de hello est à froid, représentée par la valeur de hello **0.0**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="ded7c-144">Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="ded7c-145">Configurer le pipeline d’apprentissage automatique Spark hello qui se compose de trois étapes : Générateur de jetons, hashingTF et lr.</span><span class="sxs-lookup"><span data-stu-id="ded7c-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="ded7c-146">Pour plus d’informations sur ce qu’est un pipeline et sur son fonctionnement, consultez <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span><span class="sxs-lookup"><span data-stu-id="ded7c-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="ded7c-147">Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="ded7c-148">Document de formation pipeline toohello hello adaptée.</span><span class="sxs-lookup"><span data-stu-id="ded7c-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="ded7c-149">Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="ded7c-150">Vérifiez que hello formation document toocheckpoint votre progression avec l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="ded7c-151">Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="ded7c-152">Suit toohello similaire de hello sortie doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="ded7c-152">This should give hello output similar toohello following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="ded7c-153">Revenir en arrière et vérifier la sortie hello par rapport à un fichier CSV brut hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="ded7c-154">Par exemple, hello premier ligne hello fichier CSV comporte les données :</span><span class="sxs-lookup"><span data-stu-id="ded7c-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="ded7c-155">![Capture instantanée des données de sortie pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Capture instantanée des données de sortie pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="ded7c-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="ded7c-156">Notez que la température réelle de hello est inférieure à la température de cible hello suggérant la construction de hello est à froid.</span><span class="sxs-lookup"><span data-stu-id="ded7c-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="ded7c-157">Par conséquent, dans la sortie de formation hello, hello valeur pour **étiquette** Bonjour la première ligne est **0.0**, ce qui signifie bâtiment de hello n’est pas actif.</span><span class="sxs-lookup"><span data-stu-id="ded7c-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="ded7c-158">Préparez un jeu de données toorun hello formé par rapport.</span><span class="sxs-lookup"><span data-stu-id="ded7c-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="ded7c-159">toodo par conséquent, il peut passer sur un ID système et l’âge du système (notée **SystemInfo** dans la sortie de formation hello), et le modèle de hello serait prédire hello indique si la génération avec cet âge de système et des ID système seraient être chaudes (signalées par 1.0) ou refroidissement ( signalés par 0.0).</span><span class="sxs-lookup"><span data-stu-id="ded7c-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="ded7c-160">Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="ded7c-161">Enfin, élaborer des prédictions sur les données de test hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="ded7c-162">Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="ded7c-163">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="ded7c-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="ded7c-164">À partir de hello première ligne dans une prédiction de hello, vous pouvez voir que pour un système de climatisation avec l’ID 20 et l’âge de système de 25 ans, génération de hello sera à chaud (**prédiction = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="ded7c-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="ded7c-165">Hello première valeur de DenseVector (0.49999) correspond toohello prédiction 0,0 et la valeur de seconde hello (0.5001) correspond toohello prédiction 1.0.</span><span class="sxs-lookup"><span data-stu-id="ded7c-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="ded7c-166">Dans la sortie de hello, même si la valeur de seconde hello n’est légèrement plus élevé, hello modèle montre **prédiction = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="ded7c-167">Une fois que vous avez terminé d’exécuter l’application hello, vous devez le ressources hello toorelease arrêt hello bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="ded7c-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="ded7c-168">toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.</span><span class="sxs-lookup"><span data-stu-id="ded7c-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="ded7c-169">Cette s’arrête et le bloc-notes de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="ded7c-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="ded7c-170"><a name="anaconda"></a>Utiliser une bibliothèque scikit-learn Anaconda pour le Machine Learning Spark</span><span class="sxs-lookup"><span data-stu-id="ded7c-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="ded7c-171">Les clusters Apache Spark sur HDInsight incluent des bibliothèques Anaconda,</span><span class="sxs-lookup"><span data-stu-id="ded7c-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="ded7c-172">Cela inclut également hello **scikit-en savoir plus** bibliothèque pour l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="ded7c-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="ded7c-173">bibliothèque de Hello inclut également différents jeux de données que vous pouvez utiliser les exemples d’applications toobuild directement à partir d’un bloc-notes jupyter.</span><span class="sxs-lookup"><span data-stu-id="ded7c-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="ded7c-174">Pour obtenir des exemples sur l’utilisation de hello scikit-bibliothèque de plus, consultez [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="ded7c-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="ded7c-175"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ded7c-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ded7c-176">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="ded7c-177">Scénarios</span><span class="sxs-lookup"><span data-stu-id="ded7c-177">Scenarios</span></span>
* [<span data-ttu-id="ded7c-178">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="ded7c-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ded7c-179">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ded7c-180">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="ded7c-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ded7c-181">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ded7c-182">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="ded7c-182">Create and run applications</span></span>
* [<span data-ttu-id="ded7c-183">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="ded7c-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ded7c-184">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="ded7c-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ded7c-185">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="ded7c-185">Tools and extensions</span></span>
* [<span data-ttu-id="ded7c-186">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala</span><span class="sxs-lookup"><span data-stu-id="ded7c-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ded7c-187">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="ded7c-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ded7c-188">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ded7c-189">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ded7c-190">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="ded7c-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ded7c-191">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ded7c-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ded7c-192">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="ded7c-192">Manage resources</span></span>
* [<span data-ttu-id="ded7c-193">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ded7c-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ded7c-194">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="ded7c-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
