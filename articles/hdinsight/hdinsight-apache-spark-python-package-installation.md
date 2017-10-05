---
title: "Action de script : Installer des packages Python avec Jupyter sur Azure HDInsight | Microsoft Docs"
description: "Cette section comporte des instructions détaillées expliquant comment utiliser une action de script pour configurer des blocs-notes Jupyter disponibles avec des clusters HDInsight Spark pour utiliser des packages Python externes."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="429c4-103">Utilisation d’une action de script pour installer des packages externes Python avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="429c4-104">À l’aide de la commande magique de cellule</span><span class="sxs-lookup"><span data-stu-id="429c4-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="429c4-105">À l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="429c4-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="429c4-106">Découvrez comment utiliser les actions de script pour configurer un cluster Apache Spark sur HDInsight (Linux) pour utiliser des packages **python** externes bénéficiant de la contribution de la communauté, qui ne sont pas inclus dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="429c4-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="429c4-107">Vous pouvez également configurer un bloc-notes Jupyter à l’aide de la commande magique `%%configure` pour utiliser les packages externes.</span><span class="sxs-lookup"><span data-stu-id="429c4-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="429c4-108">Pour obtenir des instructions, consultez [Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="429c4-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="429c4-109">Vous pouvez rechercher [l’index de package](https://pypi.python.org/pypi) pour obtenir la liste complète des packages disponibles.</span><span class="sxs-lookup"><span data-stu-id="429c4-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="429c4-110">Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="429c4-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="429c4-111">Par exemple, vous pouvez installer les packages mis à disposition via [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="429c4-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="429c4-112">Dans cet article, vous allez apprendre à installer le package [TensorFlow](https://www.tensorflow.org/) à l’aide de l’action de script sur votre cluster et l’utiliser via le bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="429c4-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="429c4-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="429c4-113">Prerequisites</span></span>
<span data-ttu-id="429c4-114">Vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="429c4-114">You must have the following:</span></span>

* <span data-ttu-id="429c4-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="429c4-115">An Azure subscription.</span></span> <span data-ttu-id="429c4-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="429c4-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="429c4-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="429c4-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="429c4-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="429c4-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="429c4-119">Si vous n’avez pas encore de cluster Spark sur HDInsight Linux, vous pouvez exécuter des actions de script lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="429c4-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="429c4-120">Consultez la documentation sur [Guide d’utilisation des actions de script personnalisées](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="429c4-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="429c4-121">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="429c4-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="429c4-122">Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="429c4-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="429c4-123">Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="429c4-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="429c4-124">Dans le panneau de cluster Spark, cliquez sur **Actions de script** sous **Utilisation**.</span><span class="sxs-lookup"><span data-stu-id="429c4-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="429c4-125">Exécutez l’action personnalisée qui installe TensorFlow sur les nœuds principaux et les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="429c4-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="429c4-126">Le script bash peut être référencé à partir de : https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Consultez la documentation sur [Guide d’utilisation des actions de script personnalisées](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="429c4-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="429c4-127">Il existe deux installations de Python dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="429c4-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="429c4-128">Spark utilisera l’installation d’Anaconda Python située dans `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="429c4-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="429c4-129">Référencez cette installation dans vos actions personnalisées via `/usr/bin/anaconda/bin/pip` et `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="429c4-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="429c4-130">Ouvrez un bloc-notes PySpark Jupyter</span><span class="sxs-lookup"><span data-stu-id="429c4-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="429c4-131">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="429c4-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="429c4-132">Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="429c4-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="429c4-133">Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="429c4-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="429c4-134">![Donnez un nom au bloc-notes](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Donnez un nom au bloc-notes")</span><span class="sxs-lookup"><span data-stu-id="429c4-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="429c4-135">Vous allez maintenant `import tensorflow` et exécuter un exemple hello world.</span><span class="sxs-lookup"><span data-stu-id="429c4-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="429c4-136">Code à copier :</span><span class="sxs-lookup"><span data-stu-id="429c4-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="429c4-137">Le résultat aura l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="429c4-137">The result will look like this:</span></span>
    
    <span data-ttu-id="429c4-138">![Exécution de code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Exécuter le code TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="429c4-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="429c4-139"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="429c4-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="429c4-140">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="429c4-141">Scénarios</span><span class="sxs-lookup"><span data-stu-id="429c4-141">Scenarios</span></span>
* [<span data-ttu-id="429c4-142">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="429c4-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="429c4-143">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="429c4-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="429c4-144">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="429c4-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="429c4-145">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="429c4-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="429c4-146">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="429c4-147">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="429c4-147">Create and run applications</span></span>
* [<span data-ttu-id="429c4-148">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="429c4-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="429c4-149">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="429c4-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="429c4-150">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="429c4-150">Tools and extensions</span></span>
* [<span data-ttu-id="429c4-151">Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="429c4-152">Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="429c4-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="429c4-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="429c4-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="429c4-154">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="429c4-155">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="429c4-156">Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="429c4-157">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="429c4-157">Manage resources</span></span>
* [<span data-ttu-id="429c4-158">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="429c4-159">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="429c4-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
