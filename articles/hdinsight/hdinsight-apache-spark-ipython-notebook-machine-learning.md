---
title: Utiliser des applications de Machine Learning Apache Spark sur HDInsight | Documents Microsoft
description: "Instructions détaillées sur la manière de créer des applications de Machine Learning Apache Spark sur des clusters Spark HDInsight à l’aide d’un bloc-notes Jupyter"
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
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="36a41-103">Créer des applications de Machine Learning Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="36a41-104">Découvrez comment créer une application de Machine Learning Apache Spark à l’aide d’un cluster Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a41-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="36a41-105">Cet article montre comment utiliser le bloc-notes Jupyter disponible avec le cluster pour créer et tester l’application.</span><span class="sxs-lookup"><span data-stu-id="36a41-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="36a41-106">L’application utilise l’exemple de données HVAC.csv, qui est disponible par défaut sur tous les clusters.</span><span class="sxs-lookup"><span data-stu-id="36a41-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="36a41-107">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="36a41-107">**Prerequisites:**</span></span>

<span data-ttu-id="36a41-108">Vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="36a41-108">You must have the following:</span></span>

* <span data-ttu-id="36a41-109">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a41-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="36a41-110">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="36a41-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="36a41-111"><a name="data"></a>Comprendre le jeu de données</span><span class="sxs-lookup"><span data-stu-id="36a41-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="36a41-112">Avant de créer l’application, nous devons comprendre la structure des données pour lesquelles nous la créons, et le type d’analyse que nous allons effectuer sur ces données.</span><span class="sxs-lookup"><span data-stu-id="36a41-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="36a41-113">Dans cet article, nous utilisons l’exemple de fichier de données **HVAC.csv** qui est disponible dans le compte de stockage Azure que vous avez associé au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36a41-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="36a41-114">Dans le compte de stockage, le fichier se trouve sous **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="36a41-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="36a41-115">Téléchargez et ouvrez le fichier CSV pour obtenir un instantané des données.</span><span class="sxs-lookup"><span data-stu-id="36a41-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="36a41-116">![Capture instantanée des données utilisées pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Capture instantanée des données utilisées pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="36a41-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="36a41-117">Les données indiquent la température cible et la température réelle d’un bâtiment dans lequel un système HVAC est installé.</span><span class="sxs-lookup"><span data-stu-id="36a41-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="36a41-118">Supposons que la colonne **System** représente l’ID système et que la colonne **SystemAge** représente le nombre d’années écoulées depuis la mise en place du système HVAC dans le bâtiment.</span><span class="sxs-lookup"><span data-stu-id="36a41-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="36a41-119">Nous utilisons ces données pour prédire si un bâtiment sera plus chaud ou plus froid en fonction de la température cible, étant donné un ID système et une ancienneté du système.</span><span class="sxs-lookup"><span data-stu-id="36a41-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="36a41-120"><a name="app"></a>Écrire une application de Machine Learning Spark à l’aide de Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="36a41-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="36a41-121">Dans cette application, nous utilisons un pipeline Spark ML pour effectuer une classification de documents.</span><span class="sxs-lookup"><span data-stu-id="36a41-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="36a41-122">Dans le pipeline, nous fractionnons le document en mots, que nous convertissons en vecteur de fonctionnalité numérique avant de créer un modèle de prédiction utilisant les vecteurs et étiquettes de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="36a41-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="36a41-123">Procédez comme suit pour créer l’application.</span><span class="sxs-lookup"><span data-stu-id="36a41-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="36a41-124">Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="36a41-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="36a41-125">Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="36a41-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="36a41-126">Dans le panneau du cluster Spark, cliquez sur **Tableau de bord du cluster**, puis sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="36a41-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="36a41-127">Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="36a41-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="36a41-128">Vous pouvez également atteindre le bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="36a41-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="36a41-129">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="36a41-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="36a41-130">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="36a41-130">Create a new notebook.</span></span> <span data-ttu-id="36a41-131">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="36a41-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="36a41-132">![Créer un bloc-notes Jupyter pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Créer un bloc-notes Jupyter pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="36a41-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="36a41-133">Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="36a41-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="36a41-134">Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="36a41-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="36a41-135">![Fournir un nom de bloc-notes pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fournir un nom de bloc-notes pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="36a41-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="36a41-136">Comme vous avez créé un bloc-notes à l’aide du noyau PySpark, il est inutile de créer des contextes explicitement.</span><span class="sxs-lookup"><span data-stu-id="36a41-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="36a41-137">Les contextes Spark et Hive sont automatiquement créés pour vous lorsque vous exécutez la première cellule de code.</span><span class="sxs-lookup"><span data-stu-id="36a41-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="36a41-138">Vous pouvez commencer par importer les types requis pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="36a41-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="36a41-139">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="36a41-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="36a41-140">À présent, vous devez charger les données (hvac.csv), les analyser et les utiliser pour effectuer l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="36a41-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="36a41-141">Pour ce faire, vous devez définir une fonction qui vérifie si la température réelle du bâtiment est supérieure à la température cible.</span><span class="sxs-lookup"><span data-stu-id="36a41-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="36a41-142">Si la température actuelle est supérieure, le bâtiment est chaud, ce qui est indiqué par la valeur **1,0**.</span><span class="sxs-lookup"><span data-stu-id="36a41-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="36a41-143">Si la température actuelle est inférieure, le bâtiment est froid, ce qui est indiqué par la valeur **0,0**.</span><span class="sxs-lookup"><span data-stu-id="36a41-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="36a41-144">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **Maj+Entrée**.</span><span class="sxs-lookup"><span data-stu-id="36a41-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="36a41-145">Configurez le pipeline Spark ML qui est composé de trois étapes : Tokenizer, HashingTF et LogisticRegression.</span><span class="sxs-lookup"><span data-stu-id="36a41-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="36a41-146">Pour plus d’informations sur ce qu’est un pipeline et sur son fonctionnement, consultez <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span><span class="sxs-lookup"><span data-stu-id="36a41-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="36a41-147">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **Maj+Entrée**.</span><span class="sxs-lookup"><span data-stu-id="36a41-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="36a41-148">Ajustez le pipeline au document d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="36a41-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="36a41-149">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **Maj+Entrée**.</span><span class="sxs-lookup"><span data-stu-id="36a41-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="36a41-150">Vérifiez le document d’apprentissage pour contrôler votre progression dans l’application.</span><span class="sxs-lookup"><span data-stu-id="36a41-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="36a41-151">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **Maj+Entrée**.</span><span class="sxs-lookup"><span data-stu-id="36a41-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="36a41-152">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="36a41-152">This should give the output similar to the following:</span></span>
   
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

    <span data-ttu-id="36a41-153">Revenez en arrière et vérifiez le résultat par rapport au fichier CSV brut.</span><span class="sxs-lookup"><span data-stu-id="36a41-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="36a41-154">Par exemple, la première ligne du fichier CSV contient les données suivantes :</span><span class="sxs-lookup"><span data-stu-id="36a41-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="36a41-155">![Capture instantanée des données de sortie pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Capture instantanée des données de sortie pour l’exemple de Machine Learning Spark")</span><span class="sxs-lookup"><span data-stu-id="36a41-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="36a41-156">Notez que la température réelle est inférieure à la température cible, suggérant que le bâtiment est froid.</span><span class="sxs-lookup"><span data-stu-id="36a41-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="36a41-157">De ce fait, dans le résultat, l’**étiquette** de la première ligne a pour valeur **0,0**,, ce qui signifie que le bâtiment n’est pas chaud.</span><span class="sxs-lookup"><span data-stu-id="36a41-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="36a41-158">Préparez un jeu de données sur lequel exécuter le modèle d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="36a41-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="36a41-159">Pour ce faire, nous allons passer un ID système et une ancienneté du système (indiqués par **SystemInfo** dans le résultat de l’apprentissage). Le modèle prédira si le bâtiment ayant cet ID système et cette ancienneté de système sera plus chaud (indiqué par la valeur 1,0) ou plus froid (indiqué par la valeur 0,0).</span><span class="sxs-lookup"><span data-stu-id="36a41-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="36a41-160">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **Maj+Entrée**.</span><span class="sxs-lookup"><span data-stu-id="36a41-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="36a41-161">Pour finir, effectuez des prédictions sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="36a41-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="36a41-162">Collez l’extrait de code suivant dans une cellule vide, puis appuyez sur **Maj+Entrée**.</span><span class="sxs-lookup"><span data-stu-id="36a41-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="36a41-163">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="36a41-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="36a41-164">Dans la première ligne de la prédiction, vous pouvez voir que pour un système HVAC avec l’ID 20 et une ancienneté du système de 25 ans, le bâtiment sera chaud (**prediction=1,0**).</span><span class="sxs-lookup"><span data-stu-id="36a41-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="36a41-165">La première valeur de DenseVector (0,49999) correspond à la prédiction 0.0, et la seconde valeur (0,5001) correspond à la prédiction 1.0.</span><span class="sxs-lookup"><span data-stu-id="36a41-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="36a41-166">Dans le résultat, même si la seconde valeur n’est que légèrement supérieure, le modèle indique **prediction=1,0**.</span><span class="sxs-lookup"><span data-stu-id="36a41-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="36a41-167">Une fois l’exécution de l’application terminée, arrêtez le bloc-notes pour libérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="36a41-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="36a41-168">Pour ce faire, dans le menu **Fichier** du bloc-notes, cliquez sur **Fermer et arrêter**.</span><span class="sxs-lookup"><span data-stu-id="36a41-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="36a41-169">Cette opération permet d’arrêter et de fermer le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="36a41-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="36a41-170"><a name="anaconda"></a>Utiliser une bibliothèque scikit-learn Anaconda pour le Machine Learning Spark</span><span class="sxs-lookup"><span data-stu-id="36a41-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="36a41-171">Les clusters Apache Spark sur HDInsight incluent des bibliothèques Anaconda,</span><span class="sxs-lookup"><span data-stu-id="36a41-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="36a41-172">notamment la bibliothèque **scikit-learn** pour l’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="36a41-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="36a41-173">Cette bibliothèque contient également différents jeux de données qui vous permettent de créer des exemples d’application directement à partir d’un bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="36a41-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="36a41-174">Pour obtenir des exemples d’utilisation de la bibliothèque scikit-learn, reportez-vous à [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="36a41-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="36a41-175"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="36a41-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="36a41-176">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="36a41-177">Scénarios</span><span class="sxs-lookup"><span data-stu-id="36a41-177">Scenarios</span></span>
* [<span data-ttu-id="36a41-178">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="36a41-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="36a41-179">Spark avec Machine Learning : utilisez Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="36a41-179">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="36a41-180">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="36a41-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="36a41-181">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="36a41-182">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="36a41-182">Create and run applications</span></span>
* [<span data-ttu-id="36a41-183">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="36a41-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="36a41-184">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="36a41-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="36a41-185">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="36a41-185">Tools and extensions</span></span>
* [<span data-ttu-id="36a41-186">Utilisez le plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="36a41-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="36a41-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="36a41-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="36a41-188">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="36a41-189">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="36a41-190">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="36a41-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="36a41-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="36a41-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="36a41-192">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="36a41-192">Manage resources</span></span>
* [<span data-ttu-id="36a41-193">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="36a41-194">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="36a41-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
