---
title: Microsoft Cognitive Toolkit avec Azure HDInsight Spark pour la formation approfondie | Microsoft Docs
description: "Découvrez comment un modèle entraîné de formation approfondie Microsoft Cognitive Toolkit peut être appliqué à un jeu de données avec l’API Python Spark dans un cluster Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="95c2f-103">Utiliser le modèle de formation approfondie Microsoft Cognitive Toolkit avec un cluster Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="95c2f-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="95c2f-104">Dans cet article, vous suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="95c2f-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="95c2f-105">Exécuter un script personnalisé pour installer Microsoft Cognitive Toolkit sur un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="95c2f-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="95c2f-106">Charger un bloc-notes Jupyter sur le cluster Spark pour voir comment appliquer un modèle entraîné de formation approfondie Microsoft Cognitive Toolkit aux fichiers d’un compte de Stockage Blob Azure avec [l’API Spark Python (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html).</span><span class="sxs-lookup"><span data-stu-id="95c2f-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95c2f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="95c2f-107">Prerequisites</span></span>

* <span data-ttu-id="95c2f-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-108">**An Azure subscription**.</span></span> <span data-ttu-id="95c2f-109">Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="95c2f-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="95c2f-110">Voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="95c2f-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="95c2f-111">**Cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="95c2f-112">Pour cet article, créez un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="95c2f-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="95c2f-113">Pour obtenir des instructions, consultez la page [Créer un cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="95c2f-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="95c2f-114">Comment fonctionne cette solution ?</span><span class="sxs-lookup"><span data-stu-id="95c2f-114">How does this solution flow?</span></span>

<span data-ttu-id="95c2f-115">Cette solution est divisée entre cet article et un bloc-notes Jupyter que vous chargez dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="95c2f-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="95c2f-116">Dans cet article, vous suivrez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="95c2f-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="95c2f-117">Exécuter une action de script sur un cluster HDInsight Spark pour installer Microsoft Cognitive Toolkit et les packages Python.</span><span class="sxs-lookup"><span data-stu-id="95c2f-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="95c2f-118">Charger le bloc-notes Jupyter qui exécute la solution sur le cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="95c2f-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="95c2f-119">Les étapes restantes suivantes sont traitées dans le bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="95c2f-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="95c2f-120">Charger des exemples d’images dans un RDD (Spark Resilient Distributed Dataset)</span><span class="sxs-lookup"><span data-stu-id="95c2f-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="95c2f-121">Charger des modules et prédéfinir des paramètres</span><span class="sxs-lookup"><span data-stu-id="95c2f-121">Load modules and define presets</span></span>
   - <span data-ttu-id="95c2f-122">Télécharger le jeu de données localement sur le cluster Spark</span><span class="sxs-lookup"><span data-stu-id="95c2f-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="95c2f-123">Convertir le jeu de données en RDD</span><span class="sxs-lookup"><span data-stu-id="95c2f-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="95c2f-124">Attribuer un score aux images selon un modèle Cognitive Toolkit entraîné</span><span class="sxs-lookup"><span data-stu-id="95c2f-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="95c2f-125">Télécharger le modèle Cognitive Toolkit entraîné vers le cluster Spark</span><span class="sxs-lookup"><span data-stu-id="95c2f-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="95c2f-126">Définir les fonctions utilisées par les nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="95c2f-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="95c2f-127">Attribuer un score aux images sur les nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="95c2f-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="95c2f-128">Évaluer la précision du modèle</span><span class="sxs-lookup"><span data-stu-id="95c2f-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="95c2f-129">Installer Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="95c2f-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="95c2f-130">Vous pouvez installer Microsoft Cognitive Toolkit sur un cluster Spark avec une action de script.</span><span class="sxs-lookup"><span data-stu-id="95c2f-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="95c2f-131">L’action de script utilise des scripts personnalisés pour installer sur le cluster des composants qui ne sont pas disponibles par défaut.</span><span class="sxs-lookup"><span data-stu-id="95c2f-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="95c2f-132">Vous pouvez utiliser le script personnalisé sur le Portail Azure, avec le Kit de développement logiciel (SDK) .NET HDInsight ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95c2f-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="95c2f-133">Vous pouvez également utiliser le script pour installer la boîte à outils lors de la création du cluster ou lorsque le cluster est prêt à fonctionner.</span><span class="sxs-lookup"><span data-stu-id="95c2f-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="95c2f-134">Dans cet article, nous utilisons le portail pour installer la boîte à outils une fois le cluster créé.</span><span class="sxs-lookup"><span data-stu-id="95c2f-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="95c2f-135">Pour connaître d’autres façons d’exécuter le script personnalisé, consultez la page [Personnaliser des clusters HDInsight avec une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="95c2f-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="95c2f-136">Utilisation du portail Azure</span><span class="sxs-lookup"><span data-stu-id="95c2f-136">Using the Azure Portal</span></span>

<span data-ttu-id="95c2f-137">Pour connaître les instructions liées à l’utilisation du Portail Azure pour exécuter une action de script, consultez la page [Personnaliser des clusters HDInsight avec une action de script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="95c2f-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="95c2f-138">Veillez à fournir les entrées suivantes pour installer Microsoft Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="95c2f-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="95c2f-139">Attribuez une valeur au nom de l’action de script.</span><span class="sxs-lookup"><span data-stu-id="95c2f-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="95c2f-140">Dans **URI de script bash**, entrez `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="95c2f-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="95c2f-141">Veillez à exécuter le script uniquement sur les nœuds principal et worker, et décochez les autres cases.</span><span class="sxs-lookup"><span data-stu-id="95c2f-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="95c2f-142">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="95c2f-143">Charger le bloc-notes Jupyter sur le cluster Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="95c2f-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="95c2f-144">Pour utiliser Microsoft Cognitive Toolkit avec le cluster Azure HDInsight Spark, vous devez charger le bloc-notes Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** sur le cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="95c2f-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="95c2f-145">Ce bloc-notes est disponible sur GitHub à l’adresse [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="95c2f-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="95c2f-146">Clonez le référentiel GitHub [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="95c2f-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="95c2f-147">Vous trouverez des instructions de clonage à la page [Cloner un référentiel](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="95c2f-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="95c2f-148">Sur le Portail Azure, ouvrez le panneau du cluster Spark que vous avez déjà configuré, cliquez sur **Tableau de bord du cluster**, puis sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="95c2f-149">Vous pouvez également lancer le bloc-notes Jupyter en accédant à l’URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="95c2f-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="95c2f-150">Remplacez \<clustername> par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="95c2f-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="95c2f-151">Dans le bloc-notes Jupyter, cliquez sur **Charger** dans le coin supérieur droit, puis accédez à l’emplacement où vous avez cloné le référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="95c2f-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="95c2f-152">![Charger le bloc-notes Jupyter sur le cluster Azure HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Charger le bloc-notes Jupyter sur le cluster Azure HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="95c2f-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="95c2f-153">Cliquez à nouveau sur **Charger**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="95c2f-154">Une fois le bloc-notes chargé, cliquez sur son nom, puis suivez les instructions qui se trouvent dans le bloc-notes même pour charger le jeu de données et suivre le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="95c2f-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="95c2f-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="95c2f-155">See also</span></span>
* [<span data-ttu-id="95c2f-156">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c2f-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="95c2f-157">Scénarios</span><span class="sxs-lookup"><span data-stu-id="95c2f-157">Scenarios</span></span>
* [<span data-ttu-id="95c2f-158">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="95c2f-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="95c2f-159">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="95c2f-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="95c2f-160">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="95c2f-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="95c2f-161">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="95c2f-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="95c2f-162">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c2f-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="95c2f-163">Application Insight telemetry data analysis using Spark in HDInsight (Analyse des données de télémétrie Application Insight à l’aide de Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="95c2f-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="95c2f-164">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="95c2f-164">Create and run applications</span></span>
* [<span data-ttu-id="95c2f-165">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="95c2f-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="95c2f-166">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="95c2f-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="95c2f-167">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="95c2f-167">Tools and extensions</span></span>
* [<span data-ttu-id="95c2f-168">Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="95c2f-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="95c2f-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="95c2f-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="95c2f-170">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c2f-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="95c2f-171">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c2f-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="95c2f-172">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="95c2f-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="95c2f-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="95c2f-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="95c2f-174">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="95c2f-174">Manage resources</span></span>
* [<span data-ttu-id="95c2f-175">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c2f-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="95c2f-176">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c2f-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
