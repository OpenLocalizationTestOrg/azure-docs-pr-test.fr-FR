---
title: "aaaTroubleshoot Hive à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses toocommon des questions sur l’utilisation d’Apache Hive et Azure HDInsight."
keywords: "Azure HDInsight, Hive, FAQ, guide de dépannage, questions courantes"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="f53a0-104">Résolution de problèmes Hive à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f53a0-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="f53a0-105">En savoir plus sur les questions supérieur hello et leurs résolutions lorsque vous travaillez avec des charges utiles d’Apache Hive dans Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="f53a0-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="f53a0-106">Comment exporter un metastore Hive et l’importer dans un autre cluster ?</span><span class="sxs-lookup"><span data-stu-id="f53a0-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f53a0-107">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f53a0-107">Resolution steps</span></span>

1. <span data-ttu-id="f53a0-108">Se connecter toohello HDInsight cluster à l’aide d’un client Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="f53a0-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="f53a0-109">Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="f53a0-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="f53a0-110">Exécutez hello suivant de commande de cluster HDInsight de hello à partir de laquelle vous souhaitez que le magasin de métadonnées tooexport hello :</span><span class="sxs-lookup"><span data-stu-id="f53a0-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="f53a0-111">Cette commande génère un fichier nommé alltables.sql.</span><span class="sxs-lookup"><span data-stu-id="f53a0-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="f53a0-112">Copiez hello fichier alltables.sql toohello nouveau cluster HDInsight, puis exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="f53a0-113">code Hello dans les étapes de résolution hello part du principe que les données sont des chemins d’accès sur le nouveau cluster de hello même hello en tant que chemins d’accès de données hello sur l’ancien cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f53a0-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="f53a0-114">Si les chemins d’accès des données hello sont différentes, vous pouvez modifier manuellement hello généré alltables.sql fichier tooreflect toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="f53a0-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="f53a0-115">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f53a0-115">Additional reading</span></span>

- [<span data-ttu-id="f53a0-116">Se connecter tooan HDInsight cluster à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="f53a0-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="f53a0-117">Comment localiser les journaux Hive sur un cluster ?</span><span class="sxs-lookup"><span data-stu-id="f53a0-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f53a0-118">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f53a0-118">Resolution steps</span></span>

1. <span data-ttu-id="f53a0-119">Connecter le cluster HDInsight de toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="f53a0-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f53a0-120">Pour plus d’informations, consultez la section **Documentation supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="f53a0-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="f53a0-121">journaux du client tooview Hive, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="f53a0-122">journaux de magasin de métadonnées Hive tooview, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="f53a0-123">tooview Hiveserver journaux, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="f53a0-124">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f53a0-124">Additional reading</span></span>

- [<span data-ttu-id="f53a0-125">Se connecter tooan HDInsight cluster à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="f53a0-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="f53a0-126">Comment lancer hello shell Hive avec des configurations spécifiques sur un cluster</span><span class="sxs-lookup"><span data-stu-id="f53a0-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f53a0-127">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f53a0-127">Resolution steps</span></span>

1. <span data-ttu-id="f53a0-128">Spécifiez une paire clé-valeur de configuration lorsque vous démarrez hello ruche shell.</span><span class="sxs-lookup"><span data-stu-id="f53a0-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="f53a0-129">Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="f53a0-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="f53a0-130">toolist toutes les configurations efficaces sur shell Hive, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f53a0-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="f53a0-131">Par exemple, utilisez hello suivant l’interface de commande toostart Hive avec la journalisation du débogage activée sur la console de hello :</span><span class="sxs-lookup"><span data-stu-id="f53a0-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="f53a0-132">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f53a0-132">Additional reading</span></span>

- <span data-ttu-id="f53a0-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties) (Propriétés de configuration Hive, en anglais)</span><span class="sxs-lookup"><span data-stu-id="f53a0-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)</span></span>


## <span data-ttu-id="f53a0-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Comment analyser les données de DAG Tez sur un chemin critique de cluster ?</span><span class="sxs-lookup"><span data-stu-id="f53a0-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f53a0-135">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f53a0-135">Resolution steps</span></span>
 
1. <span data-ttu-id="f53a0-136">tooanalyze un Tez Apache dirigées graphique acyclique (DAG) sur un graphique de cluster critiques, connecter le cluster HDInsight de toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="f53a0-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f53a0-137">Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="f53a0-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="f53a0-138">À l’invite de commandes, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="f53a0-139">toolist autres analyseurs qui peuvent être utilisé tooanalyze Tez DAG, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="f53a0-140">Vous devez fournir un exemple de programme en tant que premier argument de hello.</span><span class="sxs-lookup"><span data-stu-id="f53a0-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="f53a0-141">Noms de programme valides :</span><span class="sxs-lookup"><span data-stu-id="f53a0-141">Valid program names include:</span></span>
    - <span data-ttu-id="f53a0-142">**ContainerReuseAnalyzer**: Imprimer les détails de réutilisation du conteneur dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="f53a0-143">**CriticalPath**: chemin d’accès critique rechercher hello d’un groupe DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="f53a0-144">**LocalityAnalyzer**: Imprimer les détails de localité dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="f53a0-145">**ShuffleTimeAnalyzer**: analyser les détails de temps de lecture aléatoire hello dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="f53a0-146">**SkewAnalyzer**: analyser les informations de décalage hello dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="f53a0-147">**SlowNodeAnalyzer**: Imprimer les détails des nœuds dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="f53a0-148">**SlowTaskIdentifier**: Imprimer les détails des tâches lentes dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="f53a0-149">**SlowestVertexAnalyzer**: Imprimer les détails des données vertex les plus lentes dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="f53a0-150">**SpillAnalyzer**: Imprimer les détails de dépassement dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="f53a0-151">**TaskConcurrencyAnalyzer**: imprimer les détails d’accès concurrentiel de tâche hello dans un groupe DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="f53a0-152">**VertexLevelCriticalPathAnalyzer**: chemin d’accès critique rechercher hello au niveau de sommets dans un DAG</span><span class="sxs-lookup"><span data-stu-id="f53a0-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="f53a0-153">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f53a0-153">Additional reading</span></span>

- [<span data-ttu-id="f53a0-154">Se connecter tooan HDInsight cluster à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="f53a0-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="f53a0-155">Comment télécharger des données de DAG Tez à partir d’un cluster ?</span><span class="sxs-lookup"><span data-stu-id="f53a0-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="f53a0-156">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f53a0-156">Resolution steps</span></span>

<span data-ttu-id="f53a0-157">Il existe deux façons de données de Tez DAG toocollect hello :</span><span class="sxs-lookup"><span data-stu-id="f53a0-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="f53a0-158">À partir de la ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="f53a0-158">From hello command line:</span></span>
 
    <span data-ttu-id="f53a0-159">Connecter le cluster HDInsight de toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="f53a0-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f53a0-160">À l’invite de commandes hello exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f53a0-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="f53a0-161">Utilisez hello Ambari Tez vue :</span><span class="sxs-lookup"><span data-stu-id="f53a0-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="f53a0-162">Accédez à tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="f53a0-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="f53a0-163">Vue tooTez accédez (sous l’icône de vignettes hello dans le coin supérieur droit de hello).</span><span class="sxs-lookup"><span data-stu-id="f53a0-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="f53a0-164">Sélectionnez hello DAG souhaité tooview.</span><span class="sxs-lookup"><span data-stu-id="f53a0-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="f53a0-165">Select **Download data** (Télécharger les données).</span><span class="sxs-lookup"><span data-stu-id="f53a0-165">Select **Download data**.</span></span>

### <span data-ttu-id="f53a0-166"><a name="additional-reading-end"></a>Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f53a0-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="f53a0-167">Se connecter tooan HDInsight cluster à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="f53a0-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






