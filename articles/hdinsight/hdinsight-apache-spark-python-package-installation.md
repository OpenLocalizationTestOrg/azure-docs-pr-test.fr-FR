---
title: "action aaaScript - packages d’installation de Python avec Notebook sur Azure HDInsight | Documents Microsoft"
description: "Obtenir des instructions détaillées sur comment toouse script action tooconfigure Notebook ordinateurs portables avec HDInsight Spark clusters toouse des packages python externe."
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="924cc-103">Utiliser les packages de Python externes Action de Script tooinstall pour les ordinateurs portables Notebook dans les clusters Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="924cc-104">À l’aide de la commande magique de cellule</span><span class="sxs-lookup"><span data-stu-id="924cc-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="924cc-105">À l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="924cc-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="924cc-106">Découvrez comment toouse Actions de Script tooconfigure un cluster Apache Spark sur HDInsight (Linux) toouse externe, conçu par la Communauté **python** packages qui ne sont pas inclus l’emploi dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="924cc-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="924cc-107">Vous pouvez également configurer un bloc-notes jupyter à l’aide de `%%configure` magique toouse les packages externes.</span><span class="sxs-lookup"><span data-stu-id="924cc-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="924cc-108">Pour obtenir des instructions, consultez [Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="924cc-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="924cc-109">Vous pouvez rechercher hello [index du package](https://pypi.python.org/pypi) pour la liste complète des packages disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="924cc-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="924cc-110">Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="924cc-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="924cc-111">Par exemple, vous pouvez installer les packages mis à disposition via [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="924cc-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="924cc-112">Dans cet article, vous allez apprendre comment tooinstall hello [TensorFlow](https://www.tensorflow.org/) à l’aide du Script Actoin sur votre cluster et l’utiliser via un bloc-notes jupyter de hello.</span><span class="sxs-lookup"><span data-stu-id="924cc-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="924cc-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="924cc-113">Prerequisites</span></span>
<span data-ttu-id="924cc-114">Vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="924cc-114">You must have hello following:</span></span>

* <span data-ttu-id="924cc-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="924cc-115">An Azure subscription.</span></span> <span data-ttu-id="924cc-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="924cc-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="924cc-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="924cc-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="924cc-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="924cc-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="924cc-119">Si vous n’avez pas encore de cluster Spark sur HDInsight Linux, vous pouvez exécuter des actions de script lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="924cc-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="924cc-120">Consultez la documentation de hello sur [comment toouse personnalisées actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="924cc-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="924cc-121">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="924cc-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="924cc-122">À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil).</span><span class="sxs-lookup"><span data-stu-id="924cc-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="924cc-123">Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="924cc-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="924cc-124">Dans le panneau de cluster Spark hello, cliquez sur **Actions de Script** sous **utilisation**.</span><span class="sxs-lookup"><span data-stu-id="924cc-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="924cc-125">Exécuter l’action personnalisée hello qui installe TensorFlow nœuds principaux d’hello et nœuds de travail hello.</span><span class="sxs-lookup"><span data-stu-id="924cc-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="924cc-126">script d’interpréteur de commandes Hello peut être référencée à partir de : https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh visite documentation hello [comment toouse personnalisées actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="924cc-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="924cc-127">Il existe deux python installations en cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="924cc-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="924cc-128">Spark utilisera l’installation de python Anaconda hello située `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="924cc-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="924cc-129">Référencez cette installation dans vos actions personnalisées via `/usr/bin/anaconda/bin/pip` et `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="924cc-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="924cc-130">Ouvrez un bloc-notes PySpark Jupyter</span><span class="sxs-lookup"><span data-stu-id="924cc-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="924cc-131">![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="924cc-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="924cc-132">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="924cc-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="924cc-133">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="924cc-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="924cc-134">![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "fournir un nom d’ordinateur portable de hello")</span><span class="sxs-lookup"><span data-stu-id="924cc-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="924cc-135">Vous allez maintenant `import tensorflow` et exécuter un exemple hello world.</span><span class="sxs-lookup"><span data-stu-id="924cc-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="924cc-136">Code toocopy :</span><span class="sxs-lookup"><span data-stu-id="924cc-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="924cc-137">résultat de Hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="924cc-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="924cc-138">![Exécution de code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Exécuter le code TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="924cc-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="924cc-139"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="924cc-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="924cc-140">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="924cc-141">Scénarios</span><span class="sxs-lookup"><span data-stu-id="924cc-141">Scenarios</span></span>
* [<span data-ttu-id="924cc-142">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="924cc-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="924cc-143">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="924cc-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="924cc-144">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="924cc-145">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="924cc-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="924cc-146">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="924cc-147">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="924cc-147">Create and run applications</span></span>
* [<span data-ttu-id="924cc-148">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="924cc-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="924cc-149">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="924cc-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="924cc-150">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="924cc-150">Tools and extensions</span></span>
* [<span data-ttu-id="924cc-151">Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="924cc-152">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="924cc-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="924cc-153">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="924cc-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="924cc-154">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="924cc-155">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="924cc-156">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="924cc-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="924cc-157">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="924cc-157">Manage resources</span></span>
* [<span data-ttu-id="924cc-158">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="924cc-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="924cc-159">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="924cc-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
