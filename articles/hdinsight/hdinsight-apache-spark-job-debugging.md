---
title: "Déboguer des travaux Apache Spark en cours d’exécution sur Azure HDInsight | Documents Microsoft"
description: "Utilisez l’interface utilisateur YARN, l’interface utilisateur Spark et le serveur d’historique Spark pour suivre et déboguer les tâches en cours d’exécution sur un cluster Spark dans Azure HDInsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="6fccf-103">Déboguer des travaux Apache Spark en cours d’exécution sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fccf-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="6fccf-104">Cet article explique comment suivre et déboguer des travaux Spark en cours d’exécution sur des clusters HDInsight à l’aide de l’interface utilisateur YARN, de l’interface utilisateur Spark et du serveur d’historique Spark.</span><span class="sxs-lookup"><span data-stu-id="6fccf-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="6fccf-105">Nous allons lancer un travail Spark à partir d’un bloc-notes disponible avec le cluster Spark, **Machine Learning : analyse prédictive des données d’inspections alimentaires à l’aide de MLLib**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="6fccf-106">Vous pouvez utiliser les étapes ci-dessous pour effectuer le suivi d’une application que vous avez envoyée selon une autre méthode, par exemple, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fccf-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6fccf-107">Prerequisites</span></span>
<span data-ttu-id="6fccf-108">Vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6fccf-108">You must have the following:</span></span>

* <span data-ttu-id="6fccf-109">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6fccf-109">An Azure subscription.</span></span> <span data-ttu-id="6fccf-110">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6fccf-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6fccf-111">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6fccf-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="6fccf-112">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6fccf-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="6fccf-113">Vous devez normalement avoir commencé à exécuter le bloc-notes, **[Machine Learning : analyse prédictive des données d’inspections alimentaires à l’aide de MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="6fccf-114">Pour obtenir des instructions sur l’exécution de ce bloc-notes, suivez le lien.</span><span class="sxs-lookup"><span data-stu-id="6fccf-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="6fccf-115">Effectuer le suivi d’une application dans l’interface utilisateur YARN</span><span class="sxs-lookup"><span data-stu-id="6fccf-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="6fccf-116">Lancez l’interface utilisateur YARN.</span><span class="sxs-lookup"><span data-stu-id="6fccf-116">Launch the YARN UI.</span></span> <span data-ttu-id="6fccf-117">Dans le panneau du cluster, cliquez sur **Tableau de bord du cluster**, puis sur **YARN**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Lancer l’interface utilisateur Yarn](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="6fccf-119">Vous pouvez également lancer l’interface utilisateur de YARN à partir de celle d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="6fccf-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="6fccf-120">Pour lancer l’interface utilisateur d’Ambari, dans le panneau du cluster, cliquez sur **Tableau de bord du cluster**, puis sur **Tableau de bord de cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="6fccf-121">À partir de l’interface utilisateur d’Ambari, cliquez successivement sur **YARN**, **Quick Links** (Liens rapides), le gestionnaire de ressources actif et **ResourceManager UI** (IU de ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="6fccf-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="6fccf-122">Étant donné que vous avez démarré le travail Spark à l’aide des blocs-notes Jupyter, l’application porte le nom **remotesparkmagics** (nom de toutes les applications démarrées à partir du bloc-notes).</span><span class="sxs-lookup"><span data-stu-id="6fccf-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="6fccf-123">Cliquez sur l’ID d’application en regard du nom de l’application pour obtenir plus d’informations sur le travail.</span><span class="sxs-lookup"><span data-stu-id="6fccf-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="6fccf-124">Cette action lance la vue de l’application.</span><span class="sxs-lookup"><span data-stu-id="6fccf-124">This launches the application view.</span></span>
   
    ![Rechercher l’ID d’application Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="6fccf-126">Pour les applications lancées à partir des bloc-notes Jupyter, l’état est toujours **EN COURS D’EXÉCUTION** tant que vous ne fermez pas le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="6fccf-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="6fccf-127">Dans la vue de l’application, vous pouvez descendre pour rechercher les conteneurs associés à l’application et aux journaux (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="6fccf-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="6fccf-128">Vous pouvez également lancer l’interface utilisateur Spark en cliquant sur le lien qui correspond à l’ **URL de suivi**, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fccf-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Télécharger les journaux de conteneur](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="6fccf-130">Effectuer le suivi d’une application dans l’interface utilisateur Spark</span><span class="sxs-lookup"><span data-stu-id="6fccf-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="6fccf-131">Dans l’interface utilisateur Spark, vous pouvez explorer les travaux Spark générés par l’application que vous avez démarrée précédemment.</span><span class="sxs-lookup"><span data-stu-id="6fccf-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="6fccf-132">Pour lancer l’interface utilisateur Spark, dans la vue de l’application, cliquez sur le lien **URL de suivi**, comme illustré dans la capture d’écran ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6fccf-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="6fccf-133">Vous pouvez y voir tous les travaux Spark lancés par l’application en cours d’exécution dans le bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="6fccf-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Afficher les travaux Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="6fccf-135">Cliquez sur l’onglet **Exécuteurs** pour consulter les informations de traitement et de stockage pour chaque exécuteur.</span><span class="sxs-lookup"><span data-stu-id="6fccf-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="6fccf-136">Vous pouvez également récupérer la pile des appels en cliquant sur le lien **Thread Dump** .</span><span class="sxs-lookup"><span data-stu-id="6fccf-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Afficher les exécuteurs Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="6fccf-138">Cliquez sur l’onglet **Étapes** pour consulter les étapes de l’application.</span><span class="sxs-lookup"><span data-stu-id="6fccf-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Afficher les étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="6fccf-140">Chaque étape peut comporter plusieurs tâches dont vous pouvez afficher les statistiques d’exécution, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fccf-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Afficher les étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="6fccf-142">Dans la page de détails de l’étape, vous pouvez lancer la visualisation DAG.</span><span class="sxs-lookup"><span data-stu-id="6fccf-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="6fccf-143">Développez le lien **DAG Visualization** (Visualisation DAG) situé en haut de la page, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fccf-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Afficher la visualisation DAG des étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="6fccf-145">Le graphique DAG (Direct Aclyic Graph) représente les différentes étapes de l’application.</span><span class="sxs-lookup"><span data-stu-id="6fccf-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="6fccf-146">Chaque rectangle bleu dans le graphique représente une opération Spark appelée à partir de l’application.</span><span class="sxs-lookup"><span data-stu-id="6fccf-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="6fccf-147">Dans la page de détails de l’étape, vous pouvez également lancer la vue Chronologie de l’application.</span><span class="sxs-lookup"><span data-stu-id="6fccf-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="6fccf-148">Développez le lien **Event Timeline** (Chronologie de l’événement) situé en haut de la page, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fccf-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Afficher la chronologie d’événement des étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="6fccf-150">Vous obtenez les événements Spark sous la forme d’une chronologie.</span><span class="sxs-lookup"><span data-stu-id="6fccf-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="6fccf-151">La vue chronologie est disponible sur trois niveaux : entre différents travaux, dans un travail et dans une étape.</span><span class="sxs-lookup"><span data-stu-id="6fccf-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="6fccf-152">L’image ci-dessus capture la vue chronologie pour une étape donnée.</span><span class="sxs-lookup"><span data-stu-id="6fccf-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="6fccf-153">Si vous cochez la case **Activer le zoom** , vous pouvez faire défiler la vue chronologie vers la gauche et vers la droite.</span><span class="sxs-lookup"><span data-stu-id="6fccf-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="6fccf-154">Les autres onglets de l’interface utilisateur Spark fournissent également des informations utiles sur l’instance Spark.</span><span class="sxs-lookup"><span data-stu-id="6fccf-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="6fccf-155">Onglet Stockage : si votre application crée des RDD, vous trouverez des informations à ce sujet sous l’onglet Stockage.</span><span class="sxs-lookup"><span data-stu-id="6fccf-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="6fccf-156">Onglet Environnement : cet onglet fournit de nombreuses informations utiles concernant votre instance Spark, par exemple :</span><span class="sxs-lookup"><span data-stu-id="6fccf-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="6fccf-157">version de Scala ;</span><span class="sxs-lookup"><span data-stu-id="6fccf-157">Scala version</span></span>
     * <span data-ttu-id="6fccf-158">répertoire du journal des événements associé au cluster ;</span><span class="sxs-lookup"><span data-stu-id="6fccf-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="6fccf-159">nombre de cœurs d’exécuteur de l’application ;</span><span class="sxs-lookup"><span data-stu-id="6fccf-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="6fccf-160">etc.</span><span class="sxs-lookup"><span data-stu-id="6fccf-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="6fccf-161">Rechercher des informations sur les tâches terminées à l’aide du serveur d’historique Spark</span><span class="sxs-lookup"><span data-stu-id="6fccf-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="6fccf-162">Une fois qu’un travail est terminé, les informations concernant ce travail sont conservées dans le serveur d’historique Spark.</span><span class="sxs-lookup"><span data-stu-id="6fccf-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="6fccf-163">Pour lancer le serveur d’historique Spark, dans le panneau du cluster, cliquez sur **Tableau de bord du cluster**, puis cliquez sur **Serveur d’historique Spark**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Lancer le serveur d’historique Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="6fccf-165">Vous pouvez également lancer l’interface utilisateur du serveur d’historique Spark à partir de celle d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="6fccf-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="6fccf-166">Pour lancer l’interface utilisateur d’Ambari, dans le panneau du cluster, cliquez sur **Tableau de bord du cluster**, puis sur **Tableau de bord de cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6fccf-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="6fccf-167">À partir de l’interface utilisateur Ambari, cliquez sur **Spark**, **Quick Links** (Liens rapides), puis cliquez sur **Spark History Server UI** (Interface utilisateur du serveur d’historique Spark).</span><span class="sxs-lookup"><span data-stu-id="6fccf-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="6fccf-168">Les applications terminées s’affichent dans une liste.</span><span class="sxs-lookup"><span data-stu-id="6fccf-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="6fccf-169">Cliquez sur un ID d’application pour obtenir plus d’informations sur l’application.</span><span class="sxs-lookup"><span data-stu-id="6fccf-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Lancer le serveur d’historique Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="6fccf-171">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6fccf-171">See also</span></span>
*  [<span data-ttu-id="6fccf-172">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fccf-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="6fccf-173">Pour les analystes de données</span><span class="sxs-lookup"><span data-stu-id="6fccf-173">For data analysts</span></span>

* [<span data-ttu-id="6fccf-174">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="6fccf-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6fccf-175">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="6fccf-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="6fccf-176">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fccf-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="6fccf-177">Application Insight telemetry data analysis using Spark in HDInsight (Analyse des données de télémétrie Application Insight à l’aide de Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6fccf-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="6fccf-178">Utiliser Caffe sur Azure HDInsight Spark pour une formation approfondie échelonnée</span><span class="sxs-lookup"><span data-stu-id="6fccf-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="6fccf-179">Pour les développeurs Spark</span><span class="sxs-lookup"><span data-stu-id="6fccf-179">For Spark developers</span></span>

* [<span data-ttu-id="6fccf-180">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="6fccf-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6fccf-181">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="6fccf-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="6fccf-182">Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="6fccf-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6fccf-183">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="6fccf-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6fccf-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="6fccf-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="6fccf-185">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fccf-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="6fccf-186">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fccf-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6fccf-187">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="6fccf-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="6fccf-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6fccf-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


