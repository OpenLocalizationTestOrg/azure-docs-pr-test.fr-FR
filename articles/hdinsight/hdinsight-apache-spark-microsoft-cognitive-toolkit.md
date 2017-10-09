---
title: aaaMicrosoft cognitifs Toolkit avec Azure HDInsight Spark pour en savoir plus approfondie | Documents Microsoft
description: "Apprenez comment un apprentissage Microsoft cognitifs Toolkit approfondie de modèle d’apprentissage peut être appliqué tooa le jeu de données à l’aide de hello Spark Python API dans un cluster Azure HDInsight Spark."
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="000b3-103">Utiliser le modèle de formation approfondie Microsoft Cognitive Toolkit avec un cluster Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="000b3-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="000b3-104">Dans cet article, vous hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="000b3-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="000b3-105">Exécuter un script personnalisé de tooinstall Microsoft cognitifs Toolkit sur un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="000b3-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="000b3-106">Télécharger un toosee de cluster Notebook bloc-notes toohello Spark comment tooapply un formé Microsoft cognitifs Toolkit approfondie d’apprentissage toofiles de modèle dans un compte de stockage d’objets Blob Azure à l’aide de hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="000b3-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="000b3-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="000b3-107">Prerequisites</span></span>

* <span data-ttu-id="000b3-108">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="000b3-108">**An Azure subscription**.</span></span> <span data-ttu-id="000b3-109">Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="000b3-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="000b3-110">Voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="000b3-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="000b3-111">**Cluster Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="000b3-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="000b3-112">Pour cet article, créez un cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="000b3-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="000b3-113">Pour obtenir des instructions, consultez la page [Créer un cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="000b3-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="000b3-114">Comment fonctionne cette solution ?</span><span class="sxs-lookup"><span data-stu-id="000b3-114">How does this solution flow?</span></span>

<span data-ttu-id="000b3-115">Cette solution est divisée entre cet article et un bloc-notes Jupyter que vous chargez dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="000b3-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="000b3-116">Dans cet article, vous effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="000b3-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="000b3-117">Exécuter une action de script sur un cluster HDInsight Spark tooinstall des packages Microsoft cognitifs Toolkit et Python.</span><span class="sxs-lookup"><span data-stu-id="000b3-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="000b3-118">Télécharger un bloc-notes jupyter hello qui s’exécute hello solution toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="000b3-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="000b3-119">Hello les étapes suivantes sont décrites dans le bloc-notes jupyter de hello.</span><span class="sxs-lookup"><span data-stu-id="000b3-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="000b3-120">Charger des exemples d’images dans un RDD (Spark Resilient Distributed Dataset)</span><span class="sxs-lookup"><span data-stu-id="000b3-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="000b3-121">Charger des modules et prédéfinir des paramètres</span><span class="sxs-lookup"><span data-stu-id="000b3-121">Load modules and define presets</span></span>
   - <span data-ttu-id="000b3-122">Télécharger hello le jeu de données localement sur le cluster Spark de hello</span><span class="sxs-lookup"><span data-stu-id="000b3-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="000b3-123">Convertir le jeu de données de hello dans un RDD</span><span class="sxs-lookup"><span data-stu-id="000b3-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="000b3-124">Images de hello de score à l’aide d’un modèle de boîte à outils cognitifs formé</span><span class="sxs-lookup"><span data-stu-id="000b3-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="000b3-125">Télécharger le cluster Spark toohello hello formé Toolkit cognitifs modèle</span><span class="sxs-lookup"><span data-stu-id="000b3-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="000b3-126">Définir toobe fonctions utilisée par les nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="000b3-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="000b3-127">Images de score hello sur les nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="000b3-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="000b3-128">Évaluer la précision du modèle</span><span class="sxs-lookup"><span data-stu-id="000b3-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="000b3-129">Installer Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="000b3-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="000b3-130">Vous pouvez installer Microsoft Cognitive Toolkit sur un cluster Spark avec une action de script.</span><span class="sxs-lookup"><span data-stu-id="000b3-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="000b3-131">Action de script utilise des composants de tooinstall de scripts personnalisés sur le cluster hello qui ne sont pas disponibles par défaut.</span><span class="sxs-lookup"><span data-stu-id="000b3-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="000b3-132">Vous pouvez utiliser le script personnalisé hello hello portail Azure, à l’aide du Kit de développement logiciel HDInsight .NET ou à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="000b3-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="000b3-133">Vous pouvez également utiliser hello script tooinstall hello toolkit soit dans le cadre de la création du cluster, ou une fois le cluster de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="000b3-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="000b3-134">Dans cet article, nous utilisons hello tooinstall portail hello toolkit, une fois hello cluster a été créé.</span><span class="sxs-lookup"><span data-stu-id="000b3-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="000b3-135">Pour autres façons toorun hello personnalisé de script, consultez [HDInsight de personnaliser des clusters à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="000b3-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="000b3-136">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="000b3-136">Using hello Azure Portal</span></span>

<span data-ttu-id="000b3-137">Pour savoir comment toouse hello Azure Portal toorun de script action, consultez [HDInsight de personnaliser des clusters à l’aide de Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="000b3-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="000b3-138">Vérifiez que vous fournissez hello suivant entrées tooinstall Microsoft cognitifs Toolkit.</span><span class="sxs-lookup"><span data-stu-id="000b3-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="000b3-139">Fournissez une valeur pour le nom de l’action script hello.</span><span class="sxs-lookup"><span data-stu-id="000b3-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="000b3-140">Dans **URI de script bash**, entrez `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="000b3-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="000b3-141">Assurez-vous que vous exécutez les script hello uniquement sur hello noeuds head et de travail et effacer tous les hello autres cases à cocher.</span><span class="sxs-lookup"><span data-stu-id="000b3-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="000b3-142">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="000b3-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="000b3-143">Télécharger hello Notebook bloc-notes tooAzure cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="000b3-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="000b3-144">toouse hello Microsoft cognitifs Toolkit avec un cluster Azure HDInsight Spark de hello, vous devez charger bloc-notes jupyter de hello **CNTK_model_scoring_on_Spark_walkthrough.ipynb** cluster Azure HDInsight Spark de toohello.</span><span class="sxs-lookup"><span data-stu-id="000b3-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="000b3-145">Ce bloc-notes est disponible sur GitHub à l’adresse [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="000b3-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="000b3-146">Référentiel de clone hello GitHub [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="000b3-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="000b3-147">Pour obtenir des instructions tooclone, consultez [clonage d’un référentiel](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="000b3-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="000b3-148">À partir de hello portail Azure, ouvrez le panneau de cluster Spark hello que vous déjà configurée, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes jupyter**.</span><span class="sxs-lookup"><span data-stu-id="000b3-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="000b3-149">Vous pouvez également lancer bloc-notes jupyter de hello en accédant toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="000b3-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="000b3-150">Remplacez \<nom_cluster > avec le nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="000b3-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="000b3-151">Dans le bloc-notes jupyter de hello, cliquez sur **télécharger** hello en haut à droite et puis accédez emplacement toohello où vous avez cloné le référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="000b3-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="000b3-152">![Télécharger Notebook bloc-notes tooAzure cluster HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Notebook de télécharger bloc-notes tooAzure cluster HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="000b3-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="000b3-153">Cliquez à nouveau sur **Charger**.</span><span class="sxs-lookup"><span data-stu-id="000b3-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="000b3-154">Une fois que le bloc-notes de hello est téléchargé, cliquez sur nom hello de l’ordinateur portable de hello et suivez les instructions de hello dans Bloc-notes hello lui-même sur tooload hello du jeu de données et effectuer le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="000b3-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="000b3-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="000b3-155">See also</span></span>
* [<span data-ttu-id="000b3-156">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="000b3-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="000b3-157">Scénarios</span><span class="sxs-lookup"><span data-stu-id="000b3-157">Scenarios</span></span>
* [<span data-ttu-id="000b3-158">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="000b3-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="000b3-159">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="000b3-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="000b3-160">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="000b3-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="000b3-161">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="000b3-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="000b3-162">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="000b3-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="000b3-163">Application Insight telemetry data analysis using Spark in HDInsight (Analyse des données de télémétrie Application Insight à l’aide de Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="000b3-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="000b3-164">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="000b3-164">Create and run applications</span></span>
* [<span data-ttu-id="000b3-165">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="000b3-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="000b3-166">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="000b3-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="000b3-167">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="000b3-167">Tools and extensions</span></span>
* [<span data-ttu-id="000b3-168">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="000b3-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="000b3-169">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="000b3-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="000b3-170">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="000b3-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="000b3-171">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="000b3-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="000b3-172">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="000b3-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="000b3-173">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="000b3-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="000b3-174">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="000b3-174">Manage resources</span></span>
* [<span data-ttu-id="000b3-175">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="000b3-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="000b3-176">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="000b3-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
