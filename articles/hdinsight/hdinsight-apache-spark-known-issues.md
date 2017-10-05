---
title: "Résolution des problèmes liés au cluster Apache Spark dans Azure HDInsight | Microsoft Docs"
description: "En savoir plus sur les problèmes liés aux clusters Apache Spark dans Azure HDInsight et comment les résoudre."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="9271e-103">Problèmes connus du cluster Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="9271e-104">Ce document fait le suivi de tous les problèmes connus pour la version Preview publique de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9271e-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="9271e-105">Livy divulgue une session interactive</span><span class="sxs-lookup"><span data-stu-id="9271e-105">Livy leaks interactive session</span></span>
<span data-ttu-id="9271e-106">Lorsque Livy est redémarré (à partir d’Ambari ou à cause d’un redémarrage de la machine virtuelle du nœud principal 0) avec une session interactive encore active, une session de travail interactive est divulguée.</span><span class="sxs-lookup"><span data-stu-id="9271e-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="9271e-107">Pour cette raison, de nouvelles tâches peuvent rester bloquées à l’état Accepté sans pouvoir être démarrées.</span><span class="sxs-lookup"><span data-stu-id="9271e-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="9271e-108">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="9271e-108">**Mitigation:**</span></span>

<span data-ttu-id="9271e-109">Pour contourner ce problème, suivez la procédure ci-après :</span><span class="sxs-lookup"><span data-stu-id="9271e-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="9271e-110">SSH dans le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="9271e-110">Ssh into headnode.</span></span> <span data-ttu-id="9271e-111">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9271e-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9271e-112">Exécutez la commande suivante pour rechercher l’ID d’application des tâches interactives démarrées via Livy.</span><span class="sxs-lookup"><span data-stu-id="9271e-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="9271e-113">Le nom des tâches par défaut sera Livy si ces tâches ont été démarrées avec une session interactive Livy ne comportant aucun nom explicite spécifié. Pour la session Livy démarrée via le bloc-notes Jupyter, le nom de la tâche démarrera avec remotesparkmagics_*.</span><span class="sxs-lookup"><span data-stu-id="9271e-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="9271e-114">Exécutez la commande suivante pour mettre fin à ces tâches.</span><span class="sxs-lookup"><span data-stu-id="9271e-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="9271e-115">De nouvelles tâches commencent à être exécutées.</span><span class="sxs-lookup"><span data-stu-id="9271e-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="9271e-116">Serveur d’historique Spark non démarré</span><span class="sxs-lookup"><span data-stu-id="9271e-116">Spark History Server not started</span></span>
<span data-ttu-id="9271e-117">Le serveur d’historique Spark ne démarre pas automatiquement après la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="9271e-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="9271e-118">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="9271e-118">**Mitigation:**</span></span> 

<span data-ttu-id="9271e-119">Démarrez manuellement le serveur d’historique à partir d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="9271e-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="9271e-120">Problème d’autorisation dans le répertoire des journaux Spark</span><span class="sxs-lookup"><span data-stu-id="9271e-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="9271e-121">Lorsque hdiuser soumet une tâche avec spark-submit, il existe une erreur java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Autorisation refusée) et le journal du pilote n’est pas écrit.</span><span class="sxs-lookup"><span data-stu-id="9271e-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="9271e-122">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="9271e-122">**Mitigation:**</span></span>

1. <span data-ttu-id="9271e-123">Ajoutez hdiuser au groupe Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9271e-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="9271e-124">Fournissez les autorisations 777 sur /var/log/spark après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="9271e-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="9271e-125">Mettez à jour l’emplacement du journal Spark à l’aide d’Ambari pour obtenir un répertoire avec les autorisations 777.</span><span class="sxs-lookup"><span data-stu-id="9271e-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="9271e-126">Exécutez spark-submit en tant que sudo.</span><span class="sxs-lookup"><span data-stu-id="9271e-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="9271e-127">Le connecteur Spark-Phoenix n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9271e-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="9271e-128">Actuellement, le connecteur Spark-Phoenix n’est pas pris en charge avec un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9271e-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="9271e-129">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="9271e-129">**Mitigation:**</span></span>

<span data-ttu-id="9271e-130">Vous devez plutôt utiliser le connecteur Spark-HBase.</span><span class="sxs-lookup"><span data-stu-id="9271e-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="9271e-131">Pour savoir comment procéder, consultez la section relative à [l’utilisation du connecteur Spark-HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="9271e-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="9271e-132">Problèmes liés aux notebooks Jupyter</span><span class="sxs-lookup"><span data-stu-id="9271e-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="9271e-133">Voici certains problèmes connus liés aux notebooks Jupyter.</span><span class="sxs-lookup"><span data-stu-id="9271e-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="9271e-134">Notebooks avec des caractères non-ASCII dans les noms de fichiers</span><span class="sxs-lookup"><span data-stu-id="9271e-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="9271e-135">Les notebooks Jupyter qui peuvent être utilisés dans les clusters Spark HDInsight ne doivent pas contenir de caractères non-ASCII dans les noms de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9271e-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="9271e-136">Si vous essayez de télécharger un fichier, par le biais de l’interface utilisateur Jupyter, qui a un nom de fichier non-ASCII, l’opération échoue en mode silencieux (c’est-à-dire que Jupyter ne vous permet pas de télécharger le fichier, mais ne renvoie pas d’erreur visible).</span><span class="sxs-lookup"><span data-stu-id="9271e-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="9271e-137">Erreur lors du chargement de notebooks de taille supérieure</span><span class="sxs-lookup"><span data-stu-id="9271e-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="9271e-138">Vous pouvez obtenir une erreur **`Error loading notebook`** lorsque vous tentez de charger un bloc-notes de taille supérieure.</span><span class="sxs-lookup"><span data-stu-id="9271e-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="9271e-139">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="9271e-139">**Mitigation:**</span></span>

<span data-ttu-id="9271e-140">Si vous obtenez cette erreur, cela ne signifie pas que vos données sont endommagées ou perdues.</span><span class="sxs-lookup"><span data-stu-id="9271e-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="9271e-141">Vos blocs-notes sont toujours sur le disque, sous `/var/lib/jupyter`et vous pouvez exécuter SSH dans le cluster pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="9271e-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="9271e-142">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9271e-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="9271e-143">Une fois connecté au cluster à l’aide de SSH, vous pouvez copier les blocs-notes depuis le cluster vers votre ordinateur local (à l’aide de SCP ou WinSCP) pour en faire une sauvegarde afin d’éviter la perte de toutes les données importantes dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="9271e-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="9271e-144">Vous pouvez ensuite créer un tunnel SSH dans votre nœud principal sur le port 8001, afin d’accéder à Jupyter sans avoir à passer par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9271e-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="9271e-145">À partir de là, vous pouvez effacer la sortie de votre bloc-notes et l’enregistrer de nouveau pour réduire la taille du bloc-notes au minimum.</span><span class="sxs-lookup"><span data-stu-id="9271e-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="9271e-146">Pour éviter cette erreur à l’avenir, gardez en tête les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="9271e-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="9271e-147">Il est important que la taille du bloc-notes reste réduite.</span><span class="sxs-lookup"><span data-stu-id="9271e-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="9271e-148">Aucune sortie de vos travaux sous Spark qui est envoyée à Jupyter n’est conservée dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="9271e-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="9271e-149">Pour Jupyter, il est en général recommandé d’éviter l’exécution de l’élément `.collect()` sur des RDD ou trames de données larges. En revanche, si vous souhaitez lire le contenu d’un RDD, pensez à exécuter `.take()` ou `.sample()` afin que votre sortie ne devienne pas trop volumineuse.</span><span class="sxs-lookup"><span data-stu-id="9271e-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="9271e-150">En outre, lorsque vous enregistrez un bloc-notes, supprimez toutes les cellules de sortie pour réduire sa taille.</span><span class="sxs-lookup"><span data-stu-id="9271e-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="9271e-151">Démarrage du bloc-notes plus long que prévu</span><span class="sxs-lookup"><span data-stu-id="9271e-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="9271e-152">La première instruction de code du bloc-notes Jupyter avec Spark Magic peut nécessiter plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="9271e-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="9271e-153">**Explication :**</span><span class="sxs-lookup"><span data-stu-id="9271e-153">**Explanation:**</span></span>

<span data-ttu-id="9271e-154">Cela se produit lorsque la première cellule du code est exécutée.</span><span class="sxs-lookup"><span data-stu-id="9271e-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="9271e-155">En arrière-plan, la configuration de la session est lancée, et les contextes Spark, SQL et Hive sont définis.</span><span class="sxs-lookup"><span data-stu-id="9271e-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="9271e-156">Une fois ces contextes définis, la première instruction est exécutée et donne l'impression que l'instruction prend beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="9271e-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="9271e-157">Délai d’attente du bloc-notes Jupyter lors de la création de la session</span><span class="sxs-lookup"><span data-stu-id="9271e-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="9271e-158">Lorsque le cluster Spark manque de ressources, les noyaux Spark et Pyspark du bloc-notes Jupyter expirent en essayant de créer la session.</span><span class="sxs-lookup"><span data-stu-id="9271e-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="9271e-159">**Atténuations :**</span><span class="sxs-lookup"><span data-stu-id="9271e-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="9271e-160">Libérez certaines ressources de votre cluster Spark :</span><span class="sxs-lookup"><span data-stu-id="9271e-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="9271e-161">Arrêtez les autres blocs-notes Spark en allant dans le menu Fermer et Arrêter ou en cliquant sur Arrêter dans l’explorateur du bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="9271e-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="9271e-162">Arrêtez les autres applications Spark à partir de YARN.</span><span class="sxs-lookup"><span data-stu-id="9271e-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="9271e-163">Redémarrez le bloc-notes que vous tentiez de démarrer.</span><span class="sxs-lookup"><span data-stu-id="9271e-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="9271e-164">Un nombre suffisant de ressources devrait désormais être disponible pour vous permettre de créer une session.</span><span class="sxs-lookup"><span data-stu-id="9271e-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="9271e-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9271e-165">See also</span></span>
* [<span data-ttu-id="9271e-166">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="9271e-167">Scénarios</span><span class="sxs-lookup"><span data-stu-id="9271e-167">Scenarios</span></span>
* [<span data-ttu-id="9271e-168">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="9271e-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9271e-169">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="9271e-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9271e-170">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="9271e-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9271e-171">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="9271e-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9271e-172">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9271e-173">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="9271e-173">Create and run applications</span></span>
* [<span data-ttu-id="9271e-174">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="9271e-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9271e-175">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="9271e-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9271e-176">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="9271e-176">Tools and extensions</span></span>
* [<span data-ttu-id="9271e-177">Utilisez le plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="9271e-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9271e-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="9271e-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9271e-179">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9271e-180">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9271e-181">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="9271e-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9271e-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9271e-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9271e-183">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="9271e-183">Manage resources</span></span>
* [<span data-ttu-id="9271e-184">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9271e-185">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="9271e-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

