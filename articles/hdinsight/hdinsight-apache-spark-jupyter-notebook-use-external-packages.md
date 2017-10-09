---
title: "les packages Maven personnalisés aaaUse avec Notebook dans Spark sur Azure HDInsight | Documents Microsoft"
description: "Obtenir des instructions détaillées sur comment tooconfigure Notebook ordinateurs portables avec HDInsight Spark clusters toouse des packages Maven personnalisés."
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
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="a360b-103">Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a360b-104">À l’aide de la commande magique de cellule</span><span class="sxs-lookup"><span data-stu-id="a360b-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="a360b-105">À l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="a360b-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="a360b-106">Découvrez comment tooconfigure un bloc-notes jupyter cluster Apache Spark sur HDInsight toouse externe, conçu par la Communauté **maven** packages qui ne sont pas inclus l’emploi dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="a360b-107">Vous pouvez rechercher hello [référentiel de Maven](http://search.maven.org/) pour la liste complète des packages disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="a360b-108">Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="a360b-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="a360b-109">Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).</span><span class="sxs-lookup"><span data-stu-id="a360b-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="a360b-110">Dans cet article, vous allez apprendre comment toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package avec un bloc-notes jupyter de hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a360b-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a360b-111">Prerequisites</span></span>
<span data-ttu-id="a360b-112">Vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="a360b-112">You must have hello following:</span></span>

* <span data-ttu-id="a360b-113">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a360b-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a360b-114">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a360b-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="a360b-115">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="a360b-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="a360b-116">À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="a360b-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="a360b-117">Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a360b-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="a360b-118">Dans le panneau de cluster Spark hello, cliquez sur **liens rapides**, puis à partir de hello **tableau de bord de Cluster** panneau, cliquez sur **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="a360b-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="a360b-119">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a360b-120">Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="a360b-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="a360b-121">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="a360b-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="a360b-122">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="a360b-122">Create a new notebook.</span></span> <span data-ttu-id="a360b-123">Cliquez sur **Nouveau**, puis sur **Spark**.</span><span class="sxs-lookup"><span data-stu-id="a360b-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="a360b-124">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="a360b-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="a360b-125">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="a360b-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="a360b-126">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="a360b-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="a360b-127">![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "fournir un nom d’ordinateur portable de hello")</span><span class="sxs-lookup"><span data-stu-id="a360b-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="a360b-128">Vous allez utiliser hello `%%configure` tooconfigure magique hello bloc-notes toouse un lot externe.</span><span class="sxs-lookup"><span data-stu-id="a360b-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="a360b-129">Dans les ordinateurs portables qui utilisent les packages externes, assurez-vous que vous appelez hello `%%configure` magique dans la première cellule de code hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="a360b-130">Cela garantit que noyau hello est configuré toouse hello du package avant le démarrage de session de hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="a360b-131">Si vous oubliez le noyau de hello tooconfigure dans la première cellule de hello, vous pouvez utiliser hello `%%configure` avec hello `-f` paramètre, mais qui va redémarrer la session de hello et tous les cours seront perdues.</span><span class="sxs-lookup"><span data-stu-id="a360b-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="a360b-132">Version de HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-132">HDInsight version</span></span> | <span data-ttu-id="a360b-133">Commande</span><span class="sxs-lookup"><span data-stu-id="a360b-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="a360b-134">Pour HDInsight 3.3 et HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="a360b-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="a360b-135">Pour HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="a360b-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="a360b-136">extrait de code Hello ci-dessus attend des coordonnées maven hello package externe de hello dans un référentiel Central de Maven.</span><span class="sxs-lookup"><span data-stu-id="a360b-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="a360b-137">Dans cet extrait de code, `com.databricks:spark-csv_2.10:1.4.0` est coordonnée maven hello **spark-csv** package.</span><span class="sxs-lookup"><span data-stu-id="a360b-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="a360b-138">Voici comment construire des coordonnées hello pour un package.</span><span class="sxs-lookup"><span data-stu-id="a360b-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="a360b-139">a.</span><span class="sxs-lookup"><span data-stu-id="a360b-139">a.</span></span> <span data-ttu-id="a360b-140">Recherchez le package de hello Bonjour Maven référentiel.</span><span class="sxs-lookup"><span data-stu-id="a360b-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="a360b-141">Dans ce didacticiel, nous utilisons [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="a360b-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="a360b-142">b.</span><span class="sxs-lookup"><span data-stu-id="a360b-142">b.</span></span> <span data-ttu-id="a360b-143">À partir de référentiel de hello, collectez les valeurs hello pour **GroupId**, **ArtifactId**, et **Version**.</span><span class="sxs-lookup"><span data-stu-id="a360b-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="a360b-144">Assurez-vous que les valeurs hello réuni correspondent à votre cluster.</span><span class="sxs-lookup"><span data-stu-id="a360b-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="a360b-145">Dans ce cas, nous utilisons un Scala 2.10 et le package de Spark 1.4.0, mais vous devrez peut-être tooselect différentes versions pour la version appropriée de Scala ou Spark hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="a360b-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="a360b-146">Vous trouverez la version Scala hello sur votre cluster en exécutant `scala.util.Properties.versionString` sur le noyau de Spark Notebook hello ou envoyer de Spark.</span><span class="sxs-lookup"><span data-stu-id="a360b-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="a360b-147">Vous trouverez la version hello Spark sur votre cluster en exécutant `sc.version` sur les ordinateurs portables de disponible.</span><span class="sxs-lookup"><span data-stu-id="a360b-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="a360b-148">![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="a360b-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="a360b-149">c.</span><span class="sxs-lookup"><span data-stu-id="a360b-149">c.</span></span> <span data-ttu-id="a360b-150">Concaténer des valeurs hello trois, séparés par un signe deux-points (**:**).</span><span class="sxs-lookup"><span data-stu-id="a360b-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="a360b-151">Exécuter la cellule de code hello avec hello `%%configure` magique.</span><span class="sxs-lookup"><span data-stu-id="a360b-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="a360b-152">Cette opération va configurer hello sous-jacent Livy session toouse hello package fourni.</span><span class="sxs-lookup"><span data-stu-id="a360b-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="a360b-153">Dans les cellules suivantes hello dans Bloc-notes de hello, vous pouvez maintenant utiliser des package de hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a360b-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="a360b-154">Vous pouvez ensuite exécuter des extraits de code hello, comme illustré ci-dessous, tooview hello données à partir de la trame de données hello vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a360b-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="a360b-155"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a360b-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a360b-156">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a360b-157">Scénarios</span><span class="sxs-lookup"><span data-stu-id="a360b-157">Scenarios</span></span>
* [<span data-ttu-id="a360b-158">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="a360b-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a360b-159">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="a360b-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a360b-160">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a360b-161">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="a360b-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a360b-162">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a360b-163">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="a360b-163">Create and run applications</span></span>
* [<span data-ttu-id="a360b-164">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="a360b-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a360b-165">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="a360b-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a360b-166">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="a360b-166">Tools and extensions</span></span>

* [<span data-ttu-id="a360b-167">Utilisation de packages externes Python avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="a360b-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="a360b-168">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="a360b-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a360b-169">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="a360b-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a360b-170">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a360b-171">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a360b-172">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="a360b-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a360b-173">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="a360b-173">Manage resources</span></span>
* [<span data-ttu-id="a360b-174">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a360b-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a360b-175">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="a360b-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

