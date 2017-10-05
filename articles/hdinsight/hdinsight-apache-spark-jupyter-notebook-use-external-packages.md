---
title: "Utiliser des packages Maven personnalisés avec des blocs-notes Jupyter dans Spark sur Azure HDInsight | Documents Microsoft"
description: "Cette section comporte des instructions détaillées sur la façon de configurer des blocs-notes Jupyter disponibles avec des clusters Spark HDInsight pour utiliser des packages Maven personnalisés."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="c915a-103">Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c915a-104">À l’aide de la commande magique de cellule</span><span class="sxs-lookup"><span data-stu-id="c915a-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="c915a-105">À l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="c915a-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="c915a-106">Découvrez comment configurer un bloc-notes Jupyter dans un cluster Apache Spark sur HDInsight pour utiliser des packages **maven** externes bénéficiant de la contribution de la communauté, qui ne sont pas inclus dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="c915a-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="c915a-107">Vous pouvez rechercher le [référentiel Maven](http://search.maven.org/) pour obtenir la liste complète des packages disponibles.</span><span class="sxs-lookup"><span data-stu-id="c915a-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="c915a-108">Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="c915a-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="c915a-109">Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).</span><span class="sxs-lookup"><span data-stu-id="c915a-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="c915a-110">Dans cet article, vous allez apprendre à utiliser le package [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) avec le bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c915a-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c915a-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c915a-111">Prerequisites</span></span>
<span data-ttu-id="c915a-112">Vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c915a-112">You must have the following:</span></span>

* <span data-ttu-id="c915a-113">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c915a-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c915a-114">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c915a-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="c915a-115">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="c915a-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="c915a-116">Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="c915a-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="c915a-117">Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c915a-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="c915a-118">Dans le panneau du cluster Spark, cliquez sur **Liens rapides**, puis dans le panneau **Tableau de bord du cluster**, cliquez sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="c915a-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="c915a-119">Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="c915a-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c915a-120">Vous pouvez également atteindre le bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="c915a-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="c915a-121">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c915a-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="c915a-122">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="c915a-122">Create a new notebook.</span></span> <span data-ttu-id="c915a-123">Cliquez sur **Nouveau**, puis sur **Spark**.</span><span class="sxs-lookup"><span data-stu-id="c915a-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="c915a-124">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c915a-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="c915a-125">Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="c915a-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="c915a-126">Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="c915a-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="c915a-127">![Donnez un nom au bloc-notes](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Donnez un nom au bloc-notes")</span><span class="sxs-lookup"><span data-stu-id="c915a-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="c915a-128">Vous allez utiliser la commande magique `%%configure` pour configurer le bloc-notes afin d’utiliser un package externe.</span><span class="sxs-lookup"><span data-stu-id="c915a-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="c915a-129">Dans les blocs-notes utilisant des packages externes, veillez à appeler la commande magique `%%configure` dans la première cellule de code.</span><span class="sxs-lookup"><span data-stu-id="c915a-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="c915a-130">Cela garantit que le noyau est configuré pour utiliser le package avant le démarrage de la session.</span><span class="sxs-lookup"><span data-stu-id="c915a-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="c915a-131">Si vous oubliez de configurer le noyau dans la première cellule, vous pouvez utiliser `%%configure` avec le paramètre `-f`. Toutefois, cette opération redémarrera la session et entraînera la perte de toute la progression.</span><span class="sxs-lookup"><span data-stu-id="c915a-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="c915a-132">Version de HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-132">HDInsight version</span></span> | <span data-ttu-id="c915a-133">Commande</span><span class="sxs-lookup"><span data-stu-id="c915a-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="c915a-134">Pour HDInsight 3.3 et HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="c915a-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="c915a-135">Pour HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="c915a-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="c915a-136">L’extrait de code ci-dessus attend une liste de coordonnées maven pour le package externe du référentiel central Maven.</span><span class="sxs-lookup"><span data-stu-id="c915a-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="c915a-137">Dans cet extrait de code, `com.databricks:spark-csv_2.10:1.4.0` est la coordonnée maven pour le package **spark-csv** .</span><span class="sxs-lookup"><span data-stu-id="c915a-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="c915a-138">Voici comment vous construire les coordonnées d’un package.</span><span class="sxs-lookup"><span data-stu-id="c915a-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="c915a-139">a.</span><span class="sxs-lookup"><span data-stu-id="c915a-139">a.</span></span> <span data-ttu-id="c915a-140">Recherchez le package dans le référentiel Maven.</span><span class="sxs-lookup"><span data-stu-id="c915a-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="c915a-141">Dans ce didacticiel, nous utilisons [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="c915a-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="c915a-142">b.</span><span class="sxs-lookup"><span data-stu-id="c915a-142">b.</span></span> <span data-ttu-id="c915a-143">À partir du référentiel, rassemblez les valeurs pour **GroupId**, **ArtifactId** et **Version**.</span><span class="sxs-lookup"><span data-stu-id="c915a-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="c915a-144">Vérifiez que les valeurs que vous collectez correspondent à votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c915a-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="c915a-145">Dans ce cas, nous utilisons un package Scala 2.10 et Spark 1.4.0, mais il peut être nécessaire de sélectionner des versions différentes pour la version appropriée de Scala ou de Spark dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c915a-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="c915a-146">Vous pouvez trouver la version de Scala sur votre cluster en exécutant `scala.util.Properties.versionString` sur le noyau Spark Jupyter ou sur spark-submit.</span><span class="sxs-lookup"><span data-stu-id="c915a-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="c915a-147">Vous pouvez trouver la version de Spark sur votre cluster en exécutant `sc.version` sur les notebooks Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c915a-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="c915a-148">![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c915a-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="c915a-149">c.</span><span class="sxs-lookup"><span data-stu-id="c915a-149">c.</span></span> <span data-ttu-id="c915a-150">Concaténez les trois valeurs séparées par deux-points (**:**).</span><span class="sxs-lookup"><span data-stu-id="c915a-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="c915a-151">Exécutez la cellule de code avec la commande magique `%%configure` .</span><span class="sxs-lookup"><span data-stu-id="c915a-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="c915a-152">Cela configurera la session Livy sous-jacente pour utiliser le package fourni.</span><span class="sxs-lookup"><span data-stu-id="c915a-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="c915a-153">Dans les cellules suivantes du bloc-notes, vous pouvez maintenant utiliser le package, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c915a-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="c915a-154">Vous pouvez ensuite exécuter les extraits de code, comme illustré ci-dessous, pour afficher les données issues du tableau de données créé lors de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c915a-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="c915a-155"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c915a-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c915a-156">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c915a-157">Scénarios</span><span class="sxs-lookup"><span data-stu-id="c915a-157">Scenarios</span></span>
* [<span data-ttu-id="c915a-158">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="c915a-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c915a-159">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="c915a-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c915a-160">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="c915a-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c915a-161">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="c915a-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c915a-162">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c915a-163">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="c915a-163">Create and run applications</span></span>
* [<span data-ttu-id="c915a-164">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="c915a-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c915a-165">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="c915a-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c915a-166">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="c915a-166">Tools and extensions</span></span>

* [<span data-ttu-id="c915a-167">Utilisation de packages externes Python avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="c915a-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="c915a-168">Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="c915a-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c915a-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="c915a-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c915a-170">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c915a-171">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c915a-172">Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c915a-173">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="c915a-173">Manage resources</span></span>
* [<span data-ttu-id="c915a-174">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c915a-175">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c915a-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

