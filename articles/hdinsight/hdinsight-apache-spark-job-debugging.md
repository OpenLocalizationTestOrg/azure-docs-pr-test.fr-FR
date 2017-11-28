---
title: "aaaDebug Apache Spark des travaux en cours d’exécution sur Azure HDInsight | Documents Microsoft"
description: "Utiliser l’interface utilisateur des fils Spark UI, tâches et Spark historique server tootrack et de débogage en cours d’exécution sur un cluster Spark dans Azure HDInsight"
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
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="78a13-103">Déboguer des travaux Apache Spark en cours d’exécution sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a13-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="78a13-104">Dans cet article, vous allez apprendre comment tootrack et débogage et des travaux en cours d’exécution sur des clusters HDInsight à l’aide de hello fils UI, interface utilisateur Spark et hello du serveur de l’historique de Spark.</span><span class="sxs-lookup"><span data-stu-id="78a13-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="78a13-105">Pour cet article, nous allons commencer un travail Spark à l’aide d’un ordinateur portable disponible avec le cluster Spark de hello, **apprentissage : l’analyse prédictive sur les données d’inspection de produits alimentaires à l’aide de MLLib**.</span><span class="sxs-lookup"><span data-stu-id="78a13-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="78a13-106">Vous pouvez utiliser les étapes de hello ci-dessous tootrack une application que vous avez envoyé à l’aide de n’importe quel autre approche, par exemple, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="78a13-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78a13-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="78a13-107">Prerequisites</span></span>
<span data-ttu-id="78a13-108">Vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="78a13-108">You must have hello following:</span></span>

* <span data-ttu-id="78a13-109">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="78a13-109">An Azure subscription.</span></span> <span data-ttu-id="78a13-110">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="78a13-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="78a13-111">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78a13-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="78a13-112">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="78a13-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="78a13-113">Démarrez bloc-notes de hello, en cours d’exécution  **[apprentissage : l’analyse prédictive sur les données d’inspection de produits alimentaires à l’aide de MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="78a13-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="78a13-114">Pour obtenir des instructions sur la façon de toorun ce bloc-notes, suivez hello lien.</span><span class="sxs-lookup"><span data-stu-id="78a13-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="78a13-115">Effectuer le suivi d’une application Bonjour fils UI</span><span class="sxs-lookup"><span data-stu-id="78a13-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="78a13-116">Lancez hello fils UI.</span><span class="sxs-lookup"><span data-stu-id="78a13-116">Launch hello YARN UI.</span></span> <span data-ttu-id="78a13-117">Dans le panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **fils**.</span><span class="sxs-lookup"><span data-stu-id="78a13-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Lancer l’interface utilisateur Yarn](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="78a13-119">Ou bien, vous pouvez également lancer hello l’interface utilisateur des fils de hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="78a13-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="78a13-120">toolaunch hello Ambari UI, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **tableau de bord de Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="78a13-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="78a13-121">À partir de hello Ambari UI, cliquez sur **fils**, cliquez sur **liens rapides**et cliquez sur Gestionnaire de ressources actif hello, puis cliquez sur **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="78a13-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="78a13-122">Étant donné que vous avez démarré la tâche de Spark hello Notebook portables, application hello a le nom de hello **remotesparkmagics** (il s’agit de nom hello pour toutes les applications qui sont démarrées à partir d’ordinateurs portables de hello).</span><span class="sxs-lookup"><span data-stu-id="78a13-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="78a13-123">Cliquez sur ID de l’application hello contre tooget de nom d’application hello plus d’informations sur la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="78a13-124">Cette opération lance le mode d’application hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-124">This launches hello application view.</span></span>
   
    ![Rechercher l’ID d’application Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="78a13-126">Pour de telles applications lancées à partir d’ordinateurs portables de hello Notebook, état de hello est toujours **en cours d’exécution** jusqu'à ce que vous quittiez bloc-notes de hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="78a13-127">Vue d’application hello, vous pouvez descendre davantage toofind conteneurs hello associé hello hello journaux des applications et (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="78a13-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="78a13-128">Vous pouvez également lancer hello Spark UI en cliquant sur hello liaison correspondante toohello **URL de suivi**, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="78a13-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Télécharger les journaux de conteneur](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="78a13-130">Effectuer le suivi d’une application Bonjour Spark UI</span><span class="sxs-lookup"><span data-stu-id="78a13-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="78a13-131">Bonjour Spark UI, vous pouvez descendre dans les travaux de Spark hello qui est générées par l’application hello lancée précédemment.</span><span class="sxs-lookup"><span data-stu-id="78a13-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="78a13-132">toolaunch hello Spark UI, à partir de la vue d’application hello, cliquez sur le lien hello contre hello **URL de suivi**, comme illustré dans la capture d’écran hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="78a13-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="78a13-133">Vous pouvez voir tous les travaux de Spark hello qui sont lancées par l’application hello en cours d’exécution dans un bloc-notes jupyter de hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Afficher les travaux Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="78a13-135">Cliquez sur hello **exécuteurs** toosee les informations de traitement et de stockage pour chaque exécuteur de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="78a13-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="78a13-136">Vous pouvez également récupérer la pile des appels hello en cliquant sur hello **de threads de vidage** lien.</span><span class="sxs-lookup"><span data-stu-id="78a13-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Afficher les exécuteurs Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="78a13-138">Cliquez sur hello **étapes** onglet étapes de hello toosee associés application hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Afficher les étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="78a13-140">Chaque étape peut comporter plusieurs tâches dont vous pouvez afficher les statistiques d’exécution, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="78a13-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Afficher les étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="78a13-142">À partir de la page de détails de l’étape hello, vous pouvez lancer visualisation de DAG.</span><span class="sxs-lookup"><span data-stu-id="78a13-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="78a13-143">Développez hello **DAG visualisation** lier en hello haut hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="78a13-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Afficher la visualisation DAG des étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="78a13-145">DAG ou Direct Aclyic graphique représente hello différentes étapes application hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="78a13-146">Chaque zone bleue dans le graphique de hello représente une opération de Spark appelée à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="78a13-147">À partir de la page de détails de l’étape hello, vous pouvez également lancer d’affichage de la chronologie application hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="78a13-148">Développez hello **événement chronologie** lier en hello haut hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="78a13-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Afficher la chronologie d’événement des étapes Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="78a13-150">Cela affiche les événements de Spark hello sous forme de hello d’une chronologie.</span><span class="sxs-lookup"><span data-stu-id="78a13-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="78a13-151">affichage de la chronologie Hello est disponible à trois niveaux, sur les travaux, au sein d’un travail et d’une étape.</span><span class="sxs-lookup"><span data-stu-id="78a13-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="78a13-152">image Hello ci-dessus capture chronologie hello pour une étape donnée.</span><span class="sxs-lookup"><span data-stu-id="78a13-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="78a13-153">Si vous sélectionnez hello **activer le zoom avant** case à cocher, vous pouvez faire défiler gauche et droite sur l’affichage de la chronologie hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="78a13-154">Autres onglets de hello Spark UI fournissent des informations utiles sur l’instance de Spark hello également.</span><span class="sxs-lookup"><span data-stu-id="78a13-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="78a13-155">Onglet stockage - si votre application crée une RDDs, vous trouverez plus d’informations sur celles figurant dans l’onglet de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="78a13-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="78a13-156">Onglet environnement - cet onglet fournit de nombreuses informations utiles sur votre instance de Spark telles que hello</span><span class="sxs-lookup"><span data-stu-id="78a13-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="78a13-157">version de Scala ;</span><span class="sxs-lookup"><span data-stu-id="78a13-157">Scala version</span></span>
     * <span data-ttu-id="78a13-158">Répertoire de journal des événements associé au cluster de hello</span><span class="sxs-lookup"><span data-stu-id="78a13-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="78a13-159">Nombre de cœurs de l’exécuteur de l’application hello</span><span class="sxs-lookup"><span data-stu-id="78a13-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="78a13-160">etc.</span><span class="sxs-lookup"><span data-stu-id="78a13-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="78a13-161">Rechercher des informations sur les travaux terminés à l’aide de hello Spark historique serveur</span><span class="sxs-lookup"><span data-stu-id="78a13-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="78a13-162">Une fois qu’une tâche est terminée, hello plus d’informations sur les travaux hello sont conservés dans hello Spark historique serveur.</span><span class="sxs-lookup"><span data-stu-id="78a13-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="78a13-163">toolaunch hello Spark Server de l’historique, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **Spark historique Server**.</span><span class="sxs-lookup"><span data-stu-id="78a13-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Lancer le serveur d’historique Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="78a13-165">Ou bien, vous pouvez également lancer hello l’interface utilisateur du serveur Spark historique à partir de hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="78a13-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="78a13-166">toolaunch hello Ambari UI, à partir du Panneau de cluster hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **tableau de bord de Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="78a13-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="78a13-167">À partir de hello Ambari UI, cliquez sur **Spark**, cliquez sur **liens rapides**, puis cliquez sur **l’interface utilisateur du serveur Spark historique**.</span><span class="sxs-lookup"><span data-stu-id="78a13-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="78a13-168">Vous verrez toutes les applications hello terminée répertoriées.</span><span class="sxs-lookup"><span data-stu-id="78a13-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="78a13-169">Cliquez sur un toodrill de ID d’application vers le bas dans une application pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="78a13-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Lancer le serveur d’historique Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="78a13-171">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="78a13-171">See also</span></span>
*  [<span data-ttu-id="78a13-172">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a13-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="78a13-173">Pour les analystes de données</span><span class="sxs-lookup"><span data-stu-id="78a13-173">For data analysts</span></span>

* [<span data-ttu-id="78a13-174">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="78a13-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="78a13-175">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a13-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="78a13-176">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a13-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="78a13-177">Application Insight telemetry data analysis using Spark in HDInsight (Analyse des données de télémétrie Application Insight à l’aide de Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="78a13-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="78a13-178">Utiliser Caffe sur Azure HDInsight Spark pour une formation approfondie échelonnée</span><span class="sxs-lookup"><span data-stu-id="78a13-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="78a13-179">Pour les développeurs Spark</span><span class="sxs-lookup"><span data-stu-id="78a13-179">For Spark developers</span></span>

* [<span data-ttu-id="78a13-180">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="78a13-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="78a13-181">Exécution de travaux à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="78a13-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="78a13-182">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala</span><span class="sxs-lookup"><span data-stu-id="78a13-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="78a13-183">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="78a13-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="78a13-184">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="78a13-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="78a13-185">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a13-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="78a13-186">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a13-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="78a13-187">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="78a13-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="78a13-188">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="78a13-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


