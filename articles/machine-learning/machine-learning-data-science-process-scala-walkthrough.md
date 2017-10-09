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
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="126cd-103">Science des données à l’aide de Scala et Spark sur Azure</span><span class="sxs-lookup"><span data-stu-id="126cd-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="126cd-104">Cet article vous explique comment toouse Scala pour les tâches d’apprentissage automatique supervisé avec hello MLlib évolutive de Spark et Spark ML packages sur un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="126cd-105">Il vous guide à travers les tâches hello constituant hello [processus de science des données](http://aka.ms/datascienceprocess): intégrer les données et exploration, de visualisation, l’ingénierie de fonctionnalité, modélisation et la consommation de modèle.</span><span class="sxs-lookup"><span data-stu-id="126cd-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="126cd-106">les modèles de Hello dans l’article de hello incluent la régression logistique et linéaire, les forêts aléatoires et les arbres augmentés de dégradé (GBTs), en outre tootwo commun supervisé tâches d’apprentissage automatique :</span><span class="sxs-lookup"><span data-stu-id="126cd-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="126cd-107">Problème de régression : prédiction du montant de conseil hello ($) pour un voyage taxi</span><span class="sxs-lookup"><span data-stu-id="126cd-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="126cd-108">Classification binaire : prédiction de la réception d’un pourboire ou non (1/0) pour une course en taxi</span><span class="sxs-lookup"><span data-stu-id="126cd-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="126cd-109">Hello, processus de modélisation requiert la formation et évaluation sur un jeu de données de test et les mesures de précision pertinentes.</span><span class="sxs-lookup"><span data-stu-id="126cd-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="126cd-110">Dans cet article, vous pouvez apprendre comment toostore ces modèles dans le stockage Blob Azure et comment tooscore et d’évaluer leurs performances prédictive.</span><span class="sxs-lookup"><span data-stu-id="126cd-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="126cd-111">Cet article couvre également hello plus avancée des rubriques Comment toooptimize modèles à l’aide de la validation croisée et hyper-paramètre de balayage.</span><span class="sxs-lookup"><span data-stu-id="126cd-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="126cd-112">les données de salutation utilisées sont un exemple hello 2013 NYC taxi voyage et le prix du jeu de données disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="126cd-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="126cd-113">[Scala](http://www.scala-lang.org/), un langage basé sur une machine virtuelle hello, intègre les concepts de langage fonctionnelle et orientée objet.</span><span class="sxs-lookup"><span data-stu-id="126cd-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="126cd-114">Il est un langage évolutif est parfaitement adaptée toodistributed de traitement dans le cloud de hello et s’exécute sur les clusters Azure Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="126cd-115">[Spark](http://spark.apache.org/) est une infrastructure de traitement parallèle open source qui prend en charge en mémoire traitement tooboost les performances de hello big applications de données analytique.</span><span class="sxs-lookup"><span data-stu-id="126cd-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="126cd-116">moteur de traitement Spark Hello est créé pour la vitesse, la facilité d’utilisation et analytique sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="126cd-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="126cd-117">De par ses capacités de calcul distribué en mémoire, Spark constitue le choix idéal pour les algorithmes itératifs utilisés dans l'apprentissage automatique et les calculs de graphiques.</span><span class="sxs-lookup"><span data-stu-id="126cd-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="126cd-118">Hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package fournit un ensemble cohérent de haut niveau API reposant sur des données d’images qui peuvent vous aider à créer et analyser les pipelines d’apprentissage pratique.</span><span class="sxs-lookup"><span data-stu-id="126cd-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="126cd-119">[MLlib](http://spark.apache.org/mllib/) est la bibliothèque de Spark apprentissage évolutif, qui offre des fonctionnalités de modélisation toothis des environnement distribué.</span><span class="sxs-lookup"><span data-stu-id="126cd-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="126cd-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) est hello hébergés par Azure offre d’open source Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="126cd-121">Il inclut également la prise en charge pour les ordinateurs portables Jupyter Scala sur cluster Spark de hello et pouvez exécution tootransform de requêtes interactif Spark SQL, filtrer et visualiser les données stockées dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="126cd-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="126cd-122">Hello Scala extraits de code dans cet article qui fournissent des solutions de hello et affichent les graphiques appropriés hello toovisualize les données de salutation s’exécutent dans les blocs-notes Notebook installés sur des clusters de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="126cd-123">étapes de modélisation Hello dans ces rubriques ont du code qui s’affiche vous comment tootrain, évaluer, enregistrer et utiliser chaque type de modèle.</span><span class="sxs-lookup"><span data-stu-id="126cd-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="126cd-124">étapes de configuration Hello et de code dans cet article sont destinées Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="126cd-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="126cd-125">Toutefois, hello code dans cet article et hello [Scala bloc-notes Jupyter](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) sont génériques et doit fonctionner sur n’importe quel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="126cd-126">Hello le programme d’installation de cluster et les étapes de gestion peuvent être légèrement différentes de ce qui est affiché dans cet article, si vous n’utilisez pas HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="126cd-127">Pour une rubrique qui vous montre comment toocomplete de Python plutôt que Scala toouse tâches pour un processus de science des données de bout en bout, consultez [Science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="126cd-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="126cd-128">Composants requis</span><span class="sxs-lookup"><span data-stu-id="126cd-128">Prerequisites</span></span>
* <span data-ttu-id="126cd-129">Vous devez avoir un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="126cd-129">You must have an Azure subscription.</span></span> <span data-ttu-id="126cd-130">Si vous n’en avez pas, [obtenez une version d’évaluation gratuite Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="126cd-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="126cd-131">Vous avez besoin d’un hello toocomplete de cluster Azure HDInsight 3.4 Spark 1.6 procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="126cd-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="126cd-132">toocreate un cluster, consultez les instructions de hello dans [mise en route : créer Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="126cd-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="126cd-133">Définir le type de cluster hello et la version sur hello **sélectionner le Type de Cluster** menu.</span><span class="sxs-lookup"><span data-stu-id="126cd-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Configuration de type cluster HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="126cd-135">Pour obtenir une description des données de voyage hello NYC taxi et obtenir des instructions sur la façon dont tooexecute code à partir d’un bloc-notes jupyter sur cluster Spark de hello, consultez les sections pertinentes de hello dans [vue d’ensemble de science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="126cd-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="126cd-136">Exécute un bloc-notes jupyter sur cluster Spark de hello Scala du code</span><span class="sxs-lookup"><span data-stu-id="126cd-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="126cd-137">Vous pouvez lancer un bloc-notes jupyter de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="126cd-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="126cd-138">Recherchez le cluster Spark de hello sur votre tableau de bord, puis cliquez sur page de gestion tooenter hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="126cd-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="126cd-139">Ensuite, cliquez sur **tableaux de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter** bloc-notes de hello tooopen associé hello Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="126cd-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Tableau de bord de cluster et notebooks Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="126cd-141">Vous pouvez également accéder aux notebooks Jupyter à l’adresse https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="126cd-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="126cd-142">Remplacez *clustername* avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="126cd-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="126cd-143">Vous avez besoin d’un mot de passe hello pour vos blocs-notes Notebook hello de tooaccess de compte administrateur.</span><span class="sxs-lookup"><span data-stu-id="126cd-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Accédez tooJupyter portables à l’aide du nom du cluster hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="126cd-145">Sélectionnez **Scala** toosee un répertoire avec quelques exemples d’ordinateurs portables préconfigurées que hello utilisation PySpark API.</span><span class="sxs-lookup"><span data-stu-id="126cd-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="126cd-146">Hello score et modélisation de l’Exploration à l’aide du bloc-notes Scala.ipynb qui contient des exemples de code hello pour cet ensemble de rubriques de Spark est disponible sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="126cd-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="126cd-147">Vous pouvez télécharger le bloc-notes hello directement à partir de GitHub toohello server de bloc-notes Jupyter sur votre cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="126cd-148">Sur votre page d’accueil Notebook, cliquez sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="126cd-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="126cd-149">Dans l’Explorateur de fichiers hello, collez hello les URL de GitHub (contenu brut) de l’ordinateur portable de hello Scala, puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="126cd-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="126cd-150">ordinateur portable de Scala Hello est disponible à hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="126cd-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="126cd-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="126cd-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="126cd-152">Configuration : contextes Spark et Hive prédéfinis, commandes magiques Spark et bibliothèques Spark</span><span class="sxs-lookup"><span data-stu-id="126cd-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="126cd-153">Contextes Spark et Hive prédéfinis</span><span class="sxs-lookup"><span data-stu-id="126cd-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="126cd-154">les noyaux Spark Hello qui sont fournis avec les ordinateurs portables Notebook ont contextes prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="126cd-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="126cd-155">Vous n’avez pas besoin tooexplicitly ensemble hello Spark ou Hive contextes avant de commencer à utiliser avec l’application hello que vous développez.</span><span class="sxs-lookup"><span data-stu-id="126cd-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="126cd-156">Hello contextes prédéfinis sont :</span><span class="sxs-lookup"><span data-stu-id="126cd-156">hello preset contexts are:</span></span>

* <span data-ttu-id="126cd-157">`sc` pour SparkContext</span><span class="sxs-lookup"><span data-stu-id="126cd-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="126cd-158">`sqlContext` pour HiveContext</span><span class="sxs-lookup"><span data-stu-id="126cd-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="126cd-159">Commandes magiques de Spark</span><span class="sxs-lookup"><span data-stu-id="126cd-159">Spark magics</span></span>
<span data-ttu-id="126cd-160">Hello Spark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec `%%`.</span><span class="sxs-lookup"><span data-stu-id="126cd-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="126cd-161">Deux de ces commandes sont utilisées dans hello suivant des exemples de code.</span><span class="sxs-lookup"><span data-stu-id="126cd-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="126cd-162">`%%local`Spécifie que le code hello dans les lignes suivantes sera exécuté localement.</span><span class="sxs-lookup"><span data-stu-id="126cd-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="126cd-163">code de Hello doit être code Scala valide.</span><span class="sxs-lookup"><span data-stu-id="126cd-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="126cd-164">`%%sql -o <variable name>` exécute une requête Hive sur `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="126cd-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="126cd-165">Si hello `-o` paramètre est passé, résultat hello de requête de hello est conservée dans hello `%%local` contexte Scala en tant qu’une trame de données Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="126cd-166">Pour plus d’informations sur les noyaux hello Notebook blocs-notes et leurs prédéfinie « magics » que vous appelez avec `%%` (par exemple, `%%local`), consultez [noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur les clusters HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="126cd-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="126cd-167">Importer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="126cd-167">Import libraries</span></span>
<span data-ttu-id="126cd-168">Importer hello Spark, MLlib et autres bibliothèques que vous aurez besoin à l’aide de hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="126cd-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="126cd-169">Ingestion de données</span><span class="sxs-lookup"><span data-stu-id="126cd-169">Data ingestion</span></span>
<span data-ttu-id="126cd-170">première étape de Hello Bonjour processus de science des données donnée tooingest hello que vous souhaitez tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="126cd-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="126cd-171">Vous récupérez des données de hello à partir de sources externes ou des systèmes où il réside dans votre environnement de modélisation et exploration de données.</span><span class="sxs-lookup"><span data-stu-id="126cd-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="126cd-172">Dans cet article, les données de salutation que vous réception sont un exemple de 0,1 % jointes hello taxi voyage et le prix du fichier de (stocké sous forme de fichier .tsv).</span><span class="sxs-lookup"><span data-stu-id="126cd-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="126cd-173">environnement de modélisation et exploration de données Hello est Spark.</span><span class="sxs-lookup"><span data-stu-id="126cd-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="126cd-174">Cette section contient hello de toocomplete code hello après la série de tâches :</span><span class="sxs-lookup"><span data-stu-id="126cd-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="126cd-175">Définir les chemins d’accès pour le stockage des données et du modèle.</span><span class="sxs-lookup"><span data-stu-id="126cd-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="126cd-176">Lire dans hello jeu de données d’entrée (stockée sous la forme d’un fichier .tsv).</span><span class="sxs-lookup"><span data-stu-id="126cd-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="126cd-177">Définir un schéma pour les données hello et nettoyer hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="126cd-178">Créer une trame de données propre, puis la mettre en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="126cd-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="126cd-179">Enregistrer les données de salutation comme une table temporaire dans SQLContext.</span><span class="sxs-lookup"><span data-stu-id="126cd-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="126cd-180">Interroger la table de hello et importer les résultats de hello dans une trame de données.</span><span class="sxs-lookup"><span data-stu-id="126cd-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="126cd-181">Définir les chemins d’accès aux emplacements de stockage dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="126cd-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="126cd-182">Spark peut lire et écrire des tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="126cd-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="126cd-183">Vous pouvez utiliser Spark tooprocess vos données existantes et puis stocker les résultats de hello à nouveau dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="126cd-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="126cd-184">modèles de toosave ou les fichiers dans le stockage Blob, vous devez tooproperly spécifier le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="126cd-185">Conteneur par défaut de hello référence jointe cluster Spark de toohello à l’aide d’un chemin d’accès qui commence par `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="126cd-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="126cd-186">Référencez d’autres emplacements en utilisant `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="126cd-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="126cd-187">Hello exemple de code suivant spécifie emplacement hello de hello toobe de données d’entrée en lecture et un stockage tooBlob hello chemin d’accès qui est attaché toohello Spark cluster où le modèle de hello sera enregistrée.</span><span class="sxs-lookup"><span data-stu-id="126cd-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="126cd-188">Importer des données, créer un RDD et définir une trame de données selon le schéma de toohello</span><span class="sxs-lookup"><span data-stu-id="126cd-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
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


<span data-ttu-id="126cd-189">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-189">**Output:**</span></span>

<span data-ttu-id="126cd-190">Cellule de temps toorun hello : 8 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="126cd-191">Interroger la table de hello et importer les résultats dans une trame de données</span><span class="sxs-lookup"><span data-stu-id="126cd-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="126cd-192">Ensuite, table des requêtes hello des prix, les passagers et les données de l’info-bulle ; filtrer les données endommagées et américaines ; et imprimer plusieurs lignes.</span><span class="sxs-lookup"><span data-stu-id="126cd-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

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

<span data-ttu-id="126cd-193">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-193">**Output:**</span></span>

| <span data-ttu-id="126cd-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="126cd-194">fare_amount</span></span> | <span data-ttu-id="126cd-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="126cd-195">passenger_count</span></span> | <span data-ttu-id="126cd-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="126cd-196">tip_amount</span></span> | <span data-ttu-id="126cd-197">tipped</span><span class="sxs-lookup"><span data-stu-id="126cd-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="126cd-198">13,5</span><span class="sxs-lookup"><span data-stu-id="126cd-198">13.5</span></span> |<span data-ttu-id="126cd-199">1.0</span><span class="sxs-lookup"><span data-stu-id="126cd-199">1.0</span></span> |<span data-ttu-id="126cd-200">2,9</span><span class="sxs-lookup"><span data-stu-id="126cd-200">2.9</span></span> |<span data-ttu-id="126cd-201">1.0</span><span class="sxs-lookup"><span data-stu-id="126cd-201">1.0</span></span> |
|        <span data-ttu-id="126cd-202">16,0</span><span class="sxs-lookup"><span data-stu-id="126cd-202">16.0</span></span> |<span data-ttu-id="126cd-203">2.0</span><span class="sxs-lookup"><span data-stu-id="126cd-203">2.0</span></span> |<span data-ttu-id="126cd-204">3.4</span><span class="sxs-lookup"><span data-stu-id="126cd-204">3.4</span></span> |<span data-ttu-id="126cd-205">1.0</span><span class="sxs-lookup"><span data-stu-id="126cd-205">1.0</span></span> |
|        <span data-ttu-id="126cd-206">10,5</span><span class="sxs-lookup"><span data-stu-id="126cd-206">10.5</span></span> |<span data-ttu-id="126cd-207">2.0</span><span class="sxs-lookup"><span data-stu-id="126cd-207">2.0</span></span> |<span data-ttu-id="126cd-208">1.0</span><span class="sxs-lookup"><span data-stu-id="126cd-208">1.0</span></span> |<span data-ttu-id="126cd-209">1.0</span><span class="sxs-lookup"><span data-stu-id="126cd-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="126cd-210">Exploration et visualisation de données</span><span class="sxs-lookup"><span data-stu-id="126cd-210">Data exploration and visualization</span></span>
<span data-ttu-id="126cd-211">Une fois que vous importez des données de salutation dans Spark, étape suivante hello hello processus de science des données est toogain une meilleure compréhension des données hello via l’exploration et visualisation.</span><span class="sxs-lookup"><span data-stu-id="126cd-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="126cd-212">Dans cette section, vous examinez les données de salutation taxi à l’aide de requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="126cd-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="126cd-213">Ensuite, importer les résultats dans un tooplot de trame de données hello hello variables cibles et des fonctionnalités potentiels pour l’examen visuel par à l’aide de la fonctionnalité de visualisation automatique hello du bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="126cd-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="126cd-214">Utilisez local et tooplot magique de données SQL</span><span class="sxs-lookup"><span data-stu-id="126cd-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="126cd-215">Par défaut, la sortie hello de tout extrait de code que vous exécutez à partir d’un bloc-notes jupyter est disponible dans le contexte de hello de session hello qui est rendues persistantes sur les nœuds de travail hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="126cd-216">Si vous voulez toosave un toohello de nœuds de travail voyage pour chaque calcul, et que si tous les hello les données dont vous avez besoin pour votre calcul est disponible localement sur le nœud du serveur hello Notebook (qui est le nœud principal de hello), vous pouvez utiliser hello `%%local` magique code hello de toorun extrait de code sur le serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="126cd-217">**Commande magique SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="126cd-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="126cd-218">Hello du noyau de HDInsight Spark prend en charge les requêtes de HiveQL d’inline facile contre SQLContext.</span><span class="sxs-lookup"><span data-stu-id="126cd-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="126cd-219">Hello (`-o VARIABLE_NAME`) argument persiste sortie hello de la requête SQL hello en tant qu’une trame de données Pandas sur le serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="126cd-220">Cela signifie qu'est disponible en mode local de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="126cd-221">`%%local`**Commande magique**.</span><span class="sxs-lookup"><span data-stu-id="126cd-221">`%%local` **magic**.</span></span> <span data-ttu-id="126cd-222">Hello `%%local` magique exécute le code de hello localement sur le serveur hello Notebook, qui est le nœud principal de hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="126cd-223">En général, vous utilisez `%%local` magique conjointement avec hello `%%sql` magique avec hello `-o` paramètre.</span><span class="sxs-lookup"><span data-stu-id="126cd-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="126cd-224">Hello `-o` paramètre soit persistant sortie hello de requête SQL hello localement, puis `%%local` magique déclencherait hello prochain jeu de toorun d’extrait de code localement par rapport à la sortie hello de requêtes SQL hello qui est conservé localement.</span><span class="sxs-lookup"><span data-stu-id="126cd-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="126cd-225">Hello interroger des données à l’aide de SQL</span><span class="sxs-lookup"><span data-stu-id="126cd-225">Query hello data by using SQL</span></span>
<span data-ttu-id="126cd-226">Cette requête extrait des boucles de taxi hello par montant de frais, nombre de passagers et quantité d’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="126cd-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="126cd-227">Bonjour suivant de code, hello `%%local` magique crée une trame de données local, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="126cd-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="126cd-228">Vous pouvez utiliser sqlResults tooplot à l’aide de matplotlib.</span><span class="sxs-lookup"><span data-stu-id="126cd-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="126cd-229">Cette commande magique locale est utilisée plusieurs fois dans cet article.</span><span class="sxs-lookup"><span data-stu-id="126cd-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="126cd-230">Si votre jeu de données est volumineuse, veuillez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="126cd-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="126cd-231">Tracer les données hello</span><span class="sxs-lookup"><span data-stu-id="126cd-231">Plot hello data</span></span>
<span data-ttu-id="126cd-232">Vous pouvez tracer à l’aide de code Python après de la trame de données hello est dans le contexte local en tant qu’une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="126cd-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="126cd-233">noyau de Spark Hello visualise automatiquement sortie hello des requêtes SQL (HiveQL) après l’exécution de code de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="126cd-234">Vous pouvez choisir entre plusieurs types de visualisations :</span><span class="sxs-lookup"><span data-stu-id="126cd-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="126cd-235">Table</span><span class="sxs-lookup"><span data-stu-id="126cd-235">Table</span></span>
* <span data-ttu-id="126cd-236">Secteurs</span><span class="sxs-lookup"><span data-stu-id="126cd-236">Pie</span></span>
* <span data-ttu-id="126cd-237">Lignes</span><span class="sxs-lookup"><span data-stu-id="126cd-237">Line</span></span>
* <span data-ttu-id="126cd-238">Domaine</span><span class="sxs-lookup"><span data-stu-id="126cd-238">Area</span></span>
* <span data-ttu-id="126cd-239">Barres</span><span class="sxs-lookup"><span data-stu-id="126cd-239">Bar</span></span>

<span data-ttu-id="126cd-240">Voici les données de salutation tooplot hello code :</span><span class="sxs-lookup"><span data-stu-id="126cd-240">Here's hello code tooplot hello data:</span></span>

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


<span data-ttu-id="126cd-241">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-241">**Output:**</span></span>

![Histogramme de montant de pourboire](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="126cd-245">Créer des fonctions et fonctionnalités de transformation puis préparer les données à intégrer dans les fonctions de modélisation</span><span class="sxs-lookup"><span data-stu-id="126cd-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="126cd-246">Pour les fonctions de modélisation basés sur l’arborescence à partir de Spark ML et MLlib, vous avez tooprepare cible et des fonctionnalités à l’aide de diverses techniques, telles que le placement, l’indexation, à chaud de celui de codage et vectorisation.</span><span class="sxs-lookup"><span data-stu-id="126cd-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="126cd-247">Voici hello procédures toofollow dans cette section :</span><span class="sxs-lookup"><span data-stu-id="126cd-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="126cd-248">Créer une caractéristique en **regroupant** les heures dans des périodes de trafic</span><span class="sxs-lookup"><span data-stu-id="126cd-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="126cd-249">Appliquer **l’indexation et l’encodage à chaud de celui** toocategorical fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="126cd-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="126cd-250">**Échantillonner et fractionner hello jeu de données** en fractions d’apprentissage et de test.</span><span class="sxs-lookup"><span data-stu-id="126cd-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="126cd-251">**Spécifier la variable de formation et les fonctionnalités**, puis créer des jeux de données distribués résilients (RDD) ou trames de données d’entrée libellés de formation et de test indexés ou encodés à chaud</span><span class="sxs-lookup"><span data-stu-id="126cd-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="126cd-252">Automatiquement **classer et vectoriser les fonctionnalités et les cibles** toouse en tant qu’entrées pour les modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="126cd-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="126cd-253">Créer une caractéristique en regroupant les heures dans des périodes de trafic</span><span class="sxs-lookup"><span data-stu-id="126cd-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="126cd-254">Ce code montre comment les compartiments de toocreate une nouvelle fonctionnalité par le placement des heures dans le temps de trafic et comment toocache hello résultant trame de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="126cd-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="126cd-255">Lorsque les frames RDDs et les données sont utilisés à plusieurs reprises, la mise en cache entraîne des temps d’exécution tooimproved.</span><span class="sxs-lookup"><span data-stu-id="126cd-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="126cd-256">En conséquence, vous allez mettre en cache les frames RDDs et les données à plusieurs stades Bonjour procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="126cd-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="126cd-257">Indexation et encodage « à chaud » des fonctionnalités catégorielles</span><span class="sxs-lookup"><span data-stu-id="126cd-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="126cd-258">modélisation de Hello et prédire les fonctions de MLlib requièrent des fonctionnalités avec les données d’entrée catégorielles toobe indexé ou codé toouse préalable.</span><span class="sxs-lookup"><span data-stu-id="126cd-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="126cd-259">Cette section vous montre comment tooindex ou coder des fonctionnalités par catégorie pour l’entrée en hello modélisation des fonctions.</span><span class="sxs-lookup"><span data-stu-id="126cd-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="126cd-260">Vous devez tooindex ou coder vos modèles de différentes façons, selon le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="126cd-261">Par exemple, les modèles de régression logistique et linéaire nécessitent un encodage « à chaud ».</span><span class="sxs-lookup"><span data-stu-id="126cd-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="126cd-262">Par exemple, une fonction avec trois catégories peut être étendue sur trois colonnes de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="126cd-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="126cd-263">Chaque colonne contient 0 ou 1 selon la catégorie hello d’une observation.</span><span class="sxs-lookup"><span data-stu-id="126cd-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="126cd-264">MLlib fournit hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) fonction pour à chaud de celui de codage.</span><span class="sxs-lookup"><span data-stu-id="126cd-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="126cd-265">Cet encodeur est mappé à une colonne de la colonne de tooa étiquette indices de vecteurs binaire au maximum une seule une valeur.</span><span class="sxs-lookup"><span data-stu-id="126cd-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="126cd-266">Cet encodage, les algorithmes qui attendent des fonctionnalités de valeurs numériques, telles que la régression logistique, peuvent être appliqué toocategorical fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="126cd-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="126cd-267">Ici, vous transformez uniquement quatre variables tooshow obtenir des exemples, qui sont des chaînes de caractères.</span><span class="sxs-lookup"><span data-stu-id="126cd-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="126cd-268">Vous pouvez également indexer d’autres variables, telles que le jour de la semaine, représentées par des valeurs numériques, en tant que variables catégorielles.</span><span class="sxs-lookup"><span data-stu-id="126cd-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="126cd-269">Pour l’indexation, utilisez `StringIndexer()`, et pour l’encodage « à chaud », utilisez les fonctions `OneHotEncoder()` de MLlib.</span><span class="sxs-lookup"><span data-stu-id="126cd-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="126cd-270">Voici hello code tooindex et coder les fonctionnalités par catégorie :</span><span class="sxs-lookup"><span data-stu-id="126cd-270">Here is hello code tooindex and encode categorical features:</span></span>

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


<span data-ttu-id="126cd-271">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-271">**Output:**</span></span>

<span data-ttu-id="126cd-272">Cellule de temps toorun hello : 4 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="126cd-273">Échantillonner et fractionner hello le jeu de données en fractions d’apprentissage et de test</span><span class="sxs-lookup"><span data-stu-id="126cd-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="126cd-274">Ce code crée un échantillonnage aléatoire de données de salutation (25 %, dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="126cd-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="126cd-275">Bien qu’il n’est pas requis pour cet exemple en raison de la taille de toohello hello du jeu de données, hello explique également comment vous pouvez échantillonner afin que vous sachiez comment toouse pour vos propres problèmes si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="126cd-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="126cd-276">Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles.</span><span class="sxs-lookup"><span data-stu-id="126cd-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="126cd-277">Ensuite, fractionner exemple hello en une partie de la formation (dans cet exemple, 75 %) et un test partie toouse (25 %, dans cet exemple) dans la classification et la modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="126cd-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="126cd-278">Ajoutez une ligne tooeach nombre aléatoire (entre 0 et 1) (dans une colonne « rand ») qui peut être des plis de validation croisée tooselect utilisés pendant la formation.</span><span class="sxs-lookup"><span data-stu-id="126cd-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

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


<span data-ttu-id="126cd-279">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-279">**Output:**</span></span>

<span data-ttu-id="126cd-280">Cellule de temps toorun hello : 2 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="126cd-281">Spécifiez la variable de formation et les fonctionnalités puis créez des objets RDD ou trames de données d’entrée libellés de formation et de test indexés ou encodés à chaud.</span><span class="sxs-lookup"><span data-stu-id="126cd-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="126cd-282">Cette section contient le code qui vous montre comment tooindex les données de texte par catégorie comme un étiqueté pointent le type de données et comment l’encoder afin de pouvoir utiliser tootrain et test de régression logistique MLlib et d’autres modèles de classification.</span><span class="sxs-lookup"><span data-stu-id="126cd-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="126cd-283">Les objets point étiquetés sont des RDD mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes Machine Learning dans MLlib.</span><span class="sxs-lookup"><span data-stu-id="126cd-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="126cd-284">Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.</span><span class="sxs-lookup"><span data-stu-id="126cd-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="126cd-285">Dans ce code, vous spécifiez la variable de hello cible (dépendante) et hello fonctionnalités toouse tootrain des modèles.</span><span class="sxs-lookup"><span data-stu-id="126cd-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="126cd-286">Vous créez ensuite des objets RDD ou trames de données d’entrée libellés de formation et de test indexés ou encodés à chaud.</span><span class="sxs-lookup"><span data-stu-id="126cd-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

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


<span data-ttu-id="126cd-287">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-287">**Output:**</span></span>

<span data-ttu-id="126cd-288">Cellule de temps toorun hello : 4 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="126cd-289">Classer automatiquement et de vectoriser toouse des fonctionnalités et des cibles en tant qu’entrées pour les modèles d’apprentissage automatique</span><span class="sxs-lookup"><span data-stu-id="126cd-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="126cd-290">Utiliser Spark ML toocategorize hello cible et les fonctionnalités toouse dans les fonctions de modélisation basés sur l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="126cd-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="126cd-291">code de Hello effectue deux tâches :</span><span class="sxs-lookup"><span data-stu-id="126cd-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="126cd-292">Crée une binaire cible pour la classification en affectant la valeur 0 ou 1 point de données tooeach comprise entre 0 et 1 à l’aide d’une valeur de seuil de 0,5.</span><span class="sxs-lookup"><span data-stu-id="126cd-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="126cd-293">Classe automatiquement les fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="126cd-293">Automatically categorizes features.</span></span> <span data-ttu-id="126cd-294">Si nombre hello de distinctes des valeurs numériques pour n’importe quelle fonctionnalité est inférieure à 32, cette fonctionnalité est classée.</span><span class="sxs-lookup"><span data-stu-id="126cd-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="126cd-295">Voici le code hello pour ces deux tâches.</span><span class="sxs-lookup"><span data-stu-id="126cd-295">Here's hello code for these two tasks.</span></span>

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



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="126cd-296">Modèle de classification binaire : Prédire si un pourboire doit être payé ou non</span><span class="sxs-lookup"><span data-stu-id="126cd-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="126cd-297">Dans cette section, vous créez trois types de toopredict de modèles de classification binaire ou non une info-bulle doit être accordée :</span><span class="sxs-lookup"><span data-stu-id="126cd-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="126cd-298">A **modèle de régression logistique** à l’aide de hello Spark ML `LogisticRegression()` (fonction)</span><span class="sxs-lookup"><span data-stu-id="126cd-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="126cd-299">A **modèle de classification de forêt aléatoire** à l’aide de hello Spark ML `RandomForestClassifier()` (fonction)</span><span class="sxs-lookup"><span data-stu-id="126cd-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="126cd-300">A **modèle de classification d’un arbre de renforcement dégradé** à l’aide de hello MLlib `GradientBoostedTrees()` (fonction)</span><span class="sxs-lookup"><span data-stu-id="126cd-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="126cd-301">Créer un modèle de régression logistique</span><span class="sxs-lookup"><span data-stu-id="126cd-301">Create a logistic regression model</span></span>
<span data-ttu-id="126cd-302">Ensuite, créez un modèle de régression logistique à l’aide de hello Spark ML `LogisticRegression()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="126cd-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="126cd-303">Vous créez le modèle hello génération de code dans une série d’étapes :</span><span class="sxs-lookup"><span data-stu-id="126cd-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="126cd-304">**Modèle de hello train** données avec un jeu de paramètres.</span><span class="sxs-lookup"><span data-stu-id="126cd-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="126cd-305">**Évaluation du modèle de hello** sur un jeu de données de test avec les mesures.</span><span class="sxs-lookup"><span data-stu-id="126cd-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="126cd-306">**Enregistrer le modèle de hello** dans le stockage Blob de sa consommation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="126cd-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="126cd-307">**Modèle de score hello** par rapport aux données de test.</span><span class="sxs-lookup"><span data-stu-id="126cd-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="126cd-308">**Tracer les résultats hello** avec récepteur courbes de caractéristique (ROC).</span><span class="sxs-lookup"><span data-stu-id="126cd-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="126cd-309">Voici le code hello de ces procédures :</span><span class="sxs-lookup"><span data-stu-id="126cd-309">Here's hello code for these procedures:</span></span>

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

<span data-ttu-id="126cd-310">Charger, évaluer et enregistrer les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-310">Load, score, and save hello results.</span></span>

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


<span data-ttu-id="126cd-311">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-311">**Output:**</span></span>

<span data-ttu-id="126cd-312">ROC sur les données de test = 0,9827381497557599</span><span class="sxs-lookup"><span data-stu-id="126cd-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="126cd-313">Utilisation de Python sur la courbe de ROC Pandas données frames tooplot hello local.</span><span class="sxs-lookup"><span data-stu-id="126cd-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

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


<span data-ttu-id="126cd-314">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-314">**Output:**</span></span>

![Courbe ROC de remise de pourboire ou non](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="126cd-316">Créer un modèle de classification par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="126cd-316">Create a random forest classification model</span></span>
<span data-ttu-id="126cd-317">Ensuite, créez un modèle de classification de forêt aléatoire à l’aide de hello Spark ML `RandomForestClassifier()` de fonction et pour évaluer le modèle hello sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="126cd-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="126cd-318">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-318">**Output:**</span></span>

<span data-ttu-id="126cd-319">ROC sur les données de test = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="126cd-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="126cd-320">Créer un modèle de classification GBT</span><span class="sxs-lookup"><span data-stu-id="126cd-320">Create a GBT classification model</span></span>
<span data-ttu-id="126cd-321">Ensuite, créez un modèle de classification GBT à l’aide de MLlib `GradientBoostedTrees()` de fonction et pour évaluer le modèle hello sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="126cd-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="126cd-322">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-322">**Output:**</span></span>

<span data-ttu-id="126cd-323">Zone sous courbe ROC = 0,9846895479241554</span><span class="sxs-lookup"><span data-stu-id="126cd-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="126cd-324">Modèle de régression : prédire le montant du pourboire</span><span class="sxs-lookup"><span data-stu-id="126cd-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="126cd-325">Dans cette section, vous créez deux types de quantité de régression modèles toopredict hello Conseil :</span><span class="sxs-lookup"><span data-stu-id="126cd-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="126cd-326">A **modèle de régression linéaire régularisée** à l’aide de hello Spark ML `LinearRegression()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="126cd-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="126cd-327">Vous allez enregistrer le modèle de hello et évaluer le modèle hello sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="126cd-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="126cd-328">A **renforcement de dégradé de modèle de régression arborescence** à l’aide de hello Spark ML `GBTRegressor()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="126cd-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="126cd-329">Créer un modèle de régression linéaire régularisée</span><span class="sxs-lookup"><span data-stu-id="126cd-329">Create a regularized linear regression model</span></span>
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


<span data-ttu-id="126cd-330">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-330">**Output:**</span></span>

<span data-ttu-id="126cd-331">Cellule de temps toorun hello : 13 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-331">Time toorun hello cell: 13 seconds.</span></span>

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


<span data-ttu-id="126cd-332">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-332">**Output:**</span></span>

<span data-ttu-id="126cd-333">R-sqr sur les données de test = 0,5960320470835743</span><span class="sxs-lookup"><span data-stu-id="126cd-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="126cd-334">Requête suivante, hello des résultats des tests en tant qu’une trame de données et l’utiliser AutoVizWidget et matplotlib toovisualize il.</span><span class="sxs-lookup"><span data-stu-id="126cd-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="126cd-335">code de Hello crée une trame de données local à partir de la sortie de la requête hello et trace les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="126cd-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="126cd-336">Hello `%%local` magique crée une trame de données locales, `sqlResults`, que vous pouvez utiliser tooplot avec matplotlib.</span><span class="sxs-lookup"><span data-stu-id="126cd-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="126cd-337">Cette commande magique Spark est utilisée plusieurs fois lors de cet article.</span><span class="sxs-lookup"><span data-stu-id="126cd-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="126cd-338">Si la quantité de hello de données est importante, vous devez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="126cd-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="126cd-339">Créez des tracés en utilisant matplotlib de Python.</span><span class="sxs-lookup"><span data-stu-id="126cd-339">Create plots by using Python matplotlib.</span></span>

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

<span data-ttu-id="126cd-340">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-340">**Output:**</span></span>

![Montant du pourboire : réel vs. prédit](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="126cd-342">Créer un modèle de régression GBT</span><span class="sxs-lookup"><span data-stu-id="126cd-342">Create a GBT regression model</span></span>
<span data-ttu-id="126cd-343">Créer un modèle de régression GBT à l’aide de hello Spark ML `GBTRegressor()` de fonction et pour évaluer le modèle hello sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="126cd-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="126cd-344">[Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="126cd-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="126cd-345">Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte.</span><span class="sxs-lookup"><span data-stu-id="126cd-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="126cd-346">Vous pouvez utiliser les GBT pour la régression et la classification.</span><span class="sxs-lookup"><span data-stu-id="126cd-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="126cd-347">Ils gèrent les caractéristiques catégorielles, ne requièrent aucune mise à l’échelle des caractéristiques et peuvent capturer les non-linéarités ainsi que les interactions entre les caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="126cd-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="126cd-348">Vous pouvez également les utiliser dans le paramétrage de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="126cd-348">You also can use them in a multiclass-classification setting.</span></span>

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


<span data-ttu-id="126cd-349">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-349">**Output:**</span></span>

<span data-ttu-id="126cd-350">Le R-sqr de test est : 0,7655383534596654</span><span class="sxs-lookup"><span data-stu-id="126cd-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="126cd-351">Utilitaires de modélisation avancée pour l’optimisation</span><span class="sxs-lookup"><span data-stu-id="126cd-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="126cd-352">Dans cette section, vous exécutez les utilitaires Machine Learning que les développeurs utilisent souvent pour l’optimisation du modèle.</span><span class="sxs-lookup"><span data-stu-id="126cd-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="126cd-353">Plus précisément, vous pouvez optimiser les modèles Machine Learning de trois façons à l’aide du balayage paramétrique et de la validation croisée :</span><span class="sxs-lookup"><span data-stu-id="126cd-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="126cd-354">Fractionner les données de hello en jeux d’apprentissage et de validation, optimiser le modèle de hello sur un jeu d’apprentissage à l’aide de balayage des paramètres hyper et évaluer sur un ensemble de validation (régression linéaire)</span><span class="sxs-lookup"><span data-stu-id="126cd-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="126cd-355">Optimiser le modèle de hello à l’aide de la validation croisée et hyper-paramètre de balayage à l’aide CrossValidator fonction de Spark ML (classification binaire)</span><span class="sxs-lookup"><span data-stu-id="126cd-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="126cd-356">Optimiser le modèle de hello à l’aide de code personnalisé de validation croisée et le balayage des paramètres toouse n’importe quel ensemble de la fonction et de paramètre (régression linéaire) d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="126cd-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="126cd-357">**La validation croisée** est une technique qui évalue le degré un modèle formé sur un jeu connu de données généralise les fonctionnalités de hello toopredict des jeux de données sur lequel il n’a pas été effectué.</span><span class="sxs-lookup"><span data-stu-id="126cd-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="126cd-358">Bonjour une idée générale de cette technique est qu’un modèle est formé sur un jeu de données de données connues et hello exactitude des prédictions est ensuite testé sur un jeu de données indépendant.</span><span class="sxs-lookup"><span data-stu-id="126cd-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="126cd-359">Une implémentation courante est toodivide un jeu de données en *k*-prise en charge et puis effectuer l’apprentissage de modèle hello de façon alternée sur tous les mais l’un des plis de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="126cd-360">**Optimisation de Hyper-paramètre** problème hello de choisir un ensemble de paramètres hyper-pour un algorithme d’apprentissage, généralement avec comme objectif hello d’optimisation d’une mesure des performances de l’algorithme hello sur un jeu de données indépendant.</span><span class="sxs-lookup"><span data-stu-id="126cd-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="126cd-361">Un paramètre-hyper est une valeur que vous devez spécifier en dehors de la procédure de formation de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="126cd-362">Hypothèses sur les valeurs de paramètre hyper peuvent affecter la flexibilité de hello et la précision du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="126cd-363">Les arbres de décision ont hyper-paramètres, par exemple, telles que hello souhaité profondeur et nombre de feuilles dans l’arborescence de hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="126cd-364">Vous devez définir un terme de pénalité en cas d’erreur de classification pour une machine à vecteurs de support (SVM).</span><span class="sxs-lookup"><span data-stu-id="126cd-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="126cd-365">Une façon tooperform hyper-paramètre optimisation courante consiste toouse une recherche de la grille, également appelé un **balayage de paramètre**.</span><span class="sxs-lookup"><span data-stu-id="126cd-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="126cd-366">Dans une recherche de la grille, une recherche exhaustive est effectuée par le biais d’un sous-ensemble spécifié de l’espace de hyper-paramètre hello pour un algorithme d’apprentissage, les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="126cd-367">La validation croisée peut fournir un toosort de métriques de performances out produits par l’algorithme de recherche hello grille des résultats optimaux hello.</span><span class="sxs-lookup"><span data-stu-id="126cd-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="126cd-368">Si vous utilisez le balayage des paramètres hyper validation croisée, vous pouvez aider les problèmes de limite le surajustement un tootraining de données de modèle.</span><span class="sxs-lookup"><span data-stu-id="126cd-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="126cd-369">De cette manière, le modèle de hello conserve hello capacité tooapply toohello général jeu de données à partir de quels hello les données d’apprentissage ont été extraites.</span><span class="sxs-lookup"><span data-stu-id="126cd-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="126cd-370">Optimiser un modèle de régression linéaire avec le balayage paramétrique</span><span class="sxs-lookup"><span data-stu-id="126cd-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="126cd-371">Ensuite, fractionner les données en jeux d’apprentissage et de validation, utilisez hyper-balayage des paramètres sur une formation toooptimize hello modèle défini et évaluer sur un ensemble de validation (régression linéaire).</span><span class="sxs-lookup"><span data-stu-id="126cd-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

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


<span data-ttu-id="126cd-372">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-372">**Output:**</span></span>

<span data-ttu-id="126cd-373">Le R-sqr de test est : 0,6226484708501209</span><span class="sxs-lookup"><span data-stu-id="126cd-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="126cd-374">Optimiser le modèle de classification binaire hello à l’aide de la validation croisée et hyper-paramètre de balayage</span><span class="sxs-lookup"><span data-stu-id="126cd-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="126cd-375">Cette section vous montre comment toooptimize une classification binaire modèle à l’aide de la validation croisée et hyper-paramètre de balayage.</span><span class="sxs-lookup"><span data-stu-id="126cd-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="126cd-376">Cette méthode utilise hello Spark ML `CrossValidator` (fonction).</span><span class="sxs-lookup"><span data-stu-id="126cd-376">This uses hello Spark ML `CrossValidator` function.</span></span>

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


<span data-ttu-id="126cd-377">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-377">**Output:**</span></span>

<span data-ttu-id="126cd-378">Cellule de temps toorun hello : 33 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="126cd-379">Optimiser le modèle de régression linéaire hello en utilisant le code de validation croisée et le balayage des paramètres personnalisé</span><span class="sxs-lookup"><span data-stu-id="126cd-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="126cd-380">Ensuite, optimiser le modèle de hello à l’aide de code personnalisé et identifier les meilleurs paramètres de modèle hello à l’aide de critère hello de précision la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="126cd-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="126cd-381">Ensuite, créez le modèle final de hello, évaluer le modèle hello sur les données de test et enregistrer le modèle de hello dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="126cd-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="126cd-382">Enfin, charger le modèle de hello, évaluer les données de test et évaluer la précision.</span><span class="sxs-lookup"><span data-stu-id="126cd-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

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


<span data-ttu-id="126cd-383">**Output:**</span><span class="sxs-lookup"><span data-stu-id="126cd-383">**Output:**</span></span>

<span data-ttu-id="126cd-384">Cellule de temps toorun hello : 61 secondes.</span><span class="sxs-lookup"><span data-stu-id="126cd-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="126cd-385">Utiliser des modèles Machine Learning basés sur Spark générés automatiquement avec Scala</span><span class="sxs-lookup"><span data-stu-id="126cd-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="126cd-386">Pour une vue d’ensemble des rubriques qui vous guident tout au long des tâches de hello qui impliquent des processus de science des données hello dans Azure, consultez [processus de science des données équipe](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="126cd-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="126cd-387">[Procédures pas à pas du processus de science des données de l’équipe](data-science-process-walkthroughs.md) décrit d’autres procédures pas à pas bout en bout qui illustrent les étapes hello Bonjour processus de science des données équipe pour des scénarios spécifiques.</span><span class="sxs-lookup"><span data-stu-id="126cd-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="126cd-388">procédures pas à pas Hello également illustrent comment toocombine cloud et locaux outils et services dans un toocreate de flux de travail ou d’un pipeline, une application intelligente.</span><span class="sxs-lookup"><span data-stu-id="126cd-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="126cd-389">[Un score de modèles d’apprentissage intégré Spark](machine-learning-data-science-spark-model-consumption.md) vous montre comment toouse Scala code tooautomatically charger et évaluer les nouveaux jeux de données avec des modèles d’apprentissage intégré Spark et enregistrées dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="126cd-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="126cd-390">Vous pouvez de suivre les instructions hello fournies et remplacez simplement hello code Python avec le code Scala dans cet article pour la consommation automatique.</span><span class="sxs-lookup"><span data-stu-id="126cd-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

