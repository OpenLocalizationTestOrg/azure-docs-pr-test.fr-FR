---
title: "cluster de problèmes aaaTroubleshoot avec Apache Spark dans Azure HDInsight | Documents Microsoft"
description: "En savoir plus sur les problèmes connexes tooApache les clusters de Spark dans Azure HDInsight et comment toowork autour de ceux."
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
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="d051d-103">Problèmes connus du cluster Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="d051d-104">Ce document effectue le suivi de hello tous les problèmes connus relatifs hello version préliminaire publique de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d051d-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="d051d-105">Livy divulgue une session interactive</span><span class="sxs-lookup"><span data-stu-id="d051d-105">Livy leaks interactive session</span></span>
<span data-ttu-id="d051d-106">Au redémarrage Livy (à partir de Ambari ou en raison du redémarrage d’ordinateur virtuel tooheadnode 0) avec une session interactive toujours active, une session interactive des tâches est inutilisables.</span><span class="sxs-lookup"><span data-stu-id="d051d-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="d051d-107">Pour cette raison, les nouveaux travaux peut bloqué dans hello état accepté et ne peut pas être démarré.</span><span class="sxs-lookup"><span data-stu-id="d051d-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="d051d-108">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="d051d-108">**Mitigation:**</span></span>

<span data-ttu-id="d051d-109">Utilisez hello suivant le problème de procédure tooworkaround hello :</span><span class="sxs-lookup"><span data-stu-id="d051d-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="d051d-110">SSH dans le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="d051d-110">Ssh into headnode.</span></span> <span data-ttu-id="d051d-111">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d051d-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d051d-112">Exécution hello après application de commande toofind hello ID des tâches interactives de hello démarrée par le biais Livy.</span><span class="sxs-lookup"><span data-stu-id="d051d-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="d051d-113">Hello les noms de tâche par défaut sera Livy si les travaux hello ont été démarrées avec une session interactive Livy sans nom explicite spécifié pour hello session Livy démarrée par un bloc-notes jupyter, nom de la tâche hello démarre avec remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="d051d-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="d051d-114">La commande suivante d’exécution hello tookill ces travaux.</span><span class="sxs-lookup"><span data-stu-id="d051d-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="d051d-115">De nouvelles tâches commencent à être exécutées.</span><span class="sxs-lookup"><span data-stu-id="d051d-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="d051d-116">Serveur d’historique Spark non démarré</span><span class="sxs-lookup"><span data-stu-id="d051d-116">Spark History Server not started</span></span>
<span data-ttu-id="d051d-117">Le serveur d’historique Spark ne démarre pas automatiquement après la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="d051d-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="d051d-118">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="d051d-118">**Mitigation:**</span></span> 

<span data-ttu-id="d051d-119">Démarrer manuellement le serveur de l’historique de hello d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="d051d-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="d051d-120">Problème d’autorisation dans le répertoire des journaux Spark</span><span class="sxs-lookup"><span data-stu-id="d051d-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="d051d-121">Lorsque hdiuser soumet un travail avec spark-submit, est un java.io.FileNotFoundException d’erreur : /var/log/spark/sparkdriver_hdiuser.log (autorisation refusée) et hello journal du pilote n’est pas écrit.</span><span class="sxs-lookup"><span data-stu-id="d051d-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="d051d-122">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="d051d-122">**Mitigation:**</span></span>

1. <span data-ttu-id="d051d-123">Ajouter un groupe de hdiuser toohello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d051d-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="d051d-124">Fournissez les autorisations 777 sur /var/log/spark après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="d051d-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="d051d-125">Mettre à jour à l’aide de Ambari toobe un répertoire avec des 777 autorisations de l’emplacement du journal de hello spark.</span><span class="sxs-lookup"><span data-stu-id="d051d-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="d051d-126">Exécutez spark-submit en tant que sudo.</span><span class="sxs-lookup"><span data-stu-id="d051d-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="d051d-127">Le connecteur Spark-Phoenix n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d051d-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="d051d-128">Actuellement, connecteur Spark-Phoenix de hello n’est pas pris en charge avec un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d051d-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="d051d-129">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="d051d-129">**Mitigation:**</span></span>

<span data-ttu-id="d051d-130">Vous devez plutôt utiliser connecteur Spark-HBase de hello.</span><span class="sxs-lookup"><span data-stu-id="d051d-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="d051d-131">Pour obtenir des instructions, consultez [comment toouse Spark-HBase connecteur](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="d051d-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="d051d-132">Les problèmes liés à tooJupyter portables</span><span class="sxs-lookup"><span data-stu-id="d051d-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="d051d-133">Voici certains ordinateurs portables tooJupyter connexes de problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="d051d-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="d051d-134">Notebooks avec des caractères non-ASCII dans les noms de fichiers</span><span class="sxs-lookup"><span data-stu-id="d051d-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="d051d-135">Les notebooks Jupyter qui peuvent être utilisés dans les clusters Spark HDInsight ne doivent pas contenir de caractères non-ASCII dans les noms de fichiers.</span><span class="sxs-lookup"><span data-stu-id="d051d-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="d051d-136">Si vous essayez de tooupload un fichier via hello UI Jupyter qui a un nom de fichier non-ASCII, il échouera en mode silencieux (autrement dit, Notebook ne vous permettre de télécharger le fichier de hello, mais elle ne lève soit une erreur visible).</span><span class="sxs-lookup"><span data-stu-id="d051d-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="d051d-137">Erreur lors du chargement de notebooks de taille supérieure</span><span class="sxs-lookup"><span data-stu-id="d051d-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="d051d-138">Vous pouvez obtenir une erreur **`Error loading notebook`** lorsque vous tentez de charger un bloc-notes de taille supérieure.</span><span class="sxs-lookup"><span data-stu-id="d051d-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="d051d-139">**Atténuation :**</span><span class="sxs-lookup"><span data-stu-id="d051d-139">**Mitigation:**</span></span>

<span data-ttu-id="d051d-140">Si vous obtenez cette erreur, cela ne signifie pas que vos données sont endommagées ou perdues.</span><span class="sxs-lookup"><span data-stu-id="d051d-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="d051d-141">Vos blocs-notes sont toujours sur le disque dans `/var/lib/jupyter`, et vous pouvez SSH dans hello cluster tooaccess les.</span><span class="sxs-lookup"><span data-stu-id="d051d-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="d051d-142">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d051d-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="d051d-143">Une fois que vous avez connecté cluster toohello à l’aide de SSH, vous pouvez copier vos blocs-notes à partir de votre ordinateur local à cluster tooyour (à l’aide du protocole SCP ou WinSCP) en tant qu’une perte de hello tooprevent sauvegarde de toutes les données importantes dans le bloc-notes de hello.</span><span class="sxs-lookup"><span data-stu-id="d051d-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="d051d-144">Vous pouvez ensuite tunnel SSH dans votre nœud principal au niveau du port, 8001 tooaccess Notebook sans passer par la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d051d-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="d051d-145">À partir de là, vous pouvez effacer le résultat de hello de votre ordinateur portable et enregistrez à nouveau la taille de toominimize hello ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="d051d-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="d051d-146">tooprevent cette erreur se produise dans hello futur, vous devez suivre quelques meilleures pratiques :</span><span class="sxs-lookup"><span data-stu-id="d051d-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="d051d-147">Il est important tookeep taille du bloc-notes hello petit.</span><span class="sxs-lookup"><span data-stu-id="d051d-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="d051d-148">Sortie à partir de vos travaux Spark renvoyées tooJupyter est conservé dans le bloc-notes de hello.</span><span class="sxs-lookup"><span data-stu-id="d051d-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="d051d-149">Il est recommandé avec Notebook dans tooavoid général en cours d’exécution `.collect()` on RDD volumineux ou des trames de données ; en revanche, si vous souhaitez toopeek au contenu d’un RDD, envisagez d’exécuter `.take()` ou `.sample()` afin que la sortie n’obtient pas trop grande.</span><span class="sxs-lookup"><span data-stu-id="d051d-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="d051d-150">En outre, lorsque vous enregistrez un ordinateur portable, désactivez toutes les cellules tooreduce hello la taille de sortie.</span><span class="sxs-lookup"><span data-stu-id="d051d-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="d051d-151">Démarrage du bloc-notes plus long que prévu</span><span class="sxs-lookup"><span data-stu-id="d051d-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="d051d-152">La première instruction de code du bloc-notes Jupyter avec Spark Magic peut nécessiter plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="d051d-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="d051d-153">**Explication :**</span><span class="sxs-lookup"><span data-stu-id="d051d-153">**Explanation:**</span></span>

<span data-ttu-id="d051d-154">Cela se produit, car lorsque la première cellule de code hello est exécuté.</span><span class="sxs-lookup"><span data-stu-id="d051d-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="d051d-155">En arrière-plan de hello cette commande lance d’une configuration de session et Spark, SQL, et les contextes de ruche sont définies.</span><span class="sxs-lookup"><span data-stu-id="d051d-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="d051d-156">Une fois ces contextes, hello première instruction est exécutée, et cela donne l’impression hello qu’instruction de hello a eu un toocomplete beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="d051d-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="d051d-157">Délai d’attente de bloc-notes Notebook lors de la création de session de hello</span><span class="sxs-lookup"><span data-stu-id="d051d-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="d051d-158">Lorsque le cluster Spark manque de ressources, hello Spark et noyaux Pyspark dans Bloc-notes jupyter de hello expireront au délai d’expiration de session de hello toocreate lors de la tentative.</span><span class="sxs-lookup"><span data-stu-id="d051d-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="d051d-159">**Atténuations :**</span><span class="sxs-lookup"><span data-stu-id="d051d-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="d051d-160">Libérez certaines ressources de votre cluster Spark :</span><span class="sxs-lookup"><span data-stu-id="d051d-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="d051d-161">L’arrêt d’autres blocs-notes Spark par toohello de va fermer et menu d’arrêt ou en cliquant sur l’arrêt dans l’Explorateur de bloc-notes hello.</span><span class="sxs-lookup"><span data-stu-id="d051d-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="d051d-162">Arrêtez les autres applications Spark à partir de YARN.</span><span class="sxs-lookup"><span data-stu-id="d051d-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="d051d-163">Redémarrez le bloc-notes hello que vous tentiez toostart des.</span><span class="sxs-lookup"><span data-stu-id="d051d-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="d051d-164">Suffisamment de ressources doit être disponibles pour vous toocreate maintenant une session.</span><span class="sxs-lookup"><span data-stu-id="d051d-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="d051d-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d051d-165">See also</span></span>
* [<span data-ttu-id="d051d-166">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d051d-167">Scénarios</span><span class="sxs-lookup"><span data-stu-id="d051d-167">Scenarios</span></span>
* [<span data-ttu-id="d051d-168">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="d051d-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d051d-169">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="d051d-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d051d-170">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d051d-171">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="d051d-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d051d-172">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d051d-173">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="d051d-173">Create and run applications</span></span>
* [<span data-ttu-id="d051d-174">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="d051d-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d051d-175">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="d051d-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d051d-176">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="d051d-176">Tools and extensions</span></span>
* [<span data-ttu-id="d051d-177">Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala</span><span class="sxs-lookup"><span data-stu-id="d051d-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d051d-178">Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance</span><span class="sxs-lookup"><span data-stu-id="d051d-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d051d-179">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d051d-180">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d051d-181">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="d051d-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="d051d-182">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="d051d-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="d051d-183">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="d051d-183">Manage resources</span></span>
* [<span data-ttu-id="d051d-184">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d051d-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d051d-185">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d051d-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

