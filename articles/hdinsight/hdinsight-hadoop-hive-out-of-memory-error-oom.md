---
title: "Corriger une erreur de mémoire insuffisante Hive dans Azure HDInsight | Microsoft Docs"
description: "Corrigez une erreur de mémoire insuffisante Hive dans Azure HDInsight. Le scénario client implique une requête sur de nombreuses tables de grande taille."
keywords: "erreur de mémoire insuffisante, OOM, paramètres Hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: da1247070ade11f78b505524f5e970e18eb16d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="96d27-105">Corriger une erreur de mémoire insuffisante Hive dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="96d27-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="96d27-106">Découvrez comment résoudre une erreur de mémoire insuffisante dans Hive lors du traitement de tables volumineuses en configurant les paramètres de mémoire Hive.</span><span class="sxs-lookup"><span data-stu-id="96d27-106">Learn how to fix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="96d27-107">Exécuter une requête Hive sur des tables de grande taille</span><span class="sxs-lookup"><span data-stu-id="96d27-107">Run Hive query against large tables</span></span>

<span data-ttu-id="96d27-108">Un client exécute une requête Hive :</span><span class="sxs-lookup"><span data-stu-id="96d27-108">A customer ran a Hive query:</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="96d27-109">Voici quelques caractéristiques de cette requête :</span><span class="sxs-lookup"><span data-stu-id="96d27-109">Some nuances of this query:</span></span>

* <span data-ttu-id="96d27-110">T1 est un alias correspondant à une très grande table nommée TABLE1 qui comporte de nombreux  types de colonne au format de chaîne.</span><span class="sxs-lookup"><span data-stu-id="96d27-110">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="96d27-111">Les autres tables ne sont pas si volumineuses, mais elles ont un grand nombre de colonnes.</span><span class="sxs-lookup"><span data-stu-id="96d27-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="96d27-112">Toutes les tables sont associées les unes aux autres, parfois avec plusieurs colonnes dans TABLE1 et d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="96d27-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="96d27-113">La requête Hive prend fin au bout de 26 minutes sur un cluster HDInsight à 24 nœuds A3.</span><span class="sxs-lookup"><span data-stu-id="96d27-113">The Hive query took 26 minutes to finish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="96d27-114">Le client a remarqué les messages d’avertissement suivants :</span><span class="sxs-lookup"><span data-stu-id="96d27-114">The customer noticed the following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="96d27-115">En utilisant le moteur d’exécution Tez.</span><span class="sxs-lookup"><span data-stu-id="96d27-115">By using the Tez execution engine.</span></span> <span data-ttu-id="96d27-116">La même requête a fonctionné pendant 15 minutes, puis a renvoyé l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="96d27-116">The same query ran for 15 minutes, and then threw the following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="96d27-117">L’erreur persiste lors de l’utilisation d’une machine virtuelle plus grande (par exemple, D12).</span><span class="sxs-lookup"><span data-stu-id="96d27-117">The error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-the-out-of-memory-error"></a><span data-ttu-id="96d27-118">Déboguer l’erreur de mémoire insuffisante</span><span class="sxs-lookup"><span data-stu-id="96d27-118">Debug the out of memory error</span></span>

<span data-ttu-id="96d27-119">Nos équipes d’ingénierie et de support technique ont trouvé qu’un des problèmes à l’origine de l’erreur de mémoire insuffisante était [décrit dans Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306) :</span><span class="sxs-lookup"><span data-stu-id="96d27-119">Our support and engineering teams together found one of the issues causing the out of memory error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="96d27-120">**hive.auto.convert.join.noconditionaltask** dans le fichier hive-site.xml avait la valeur **true** :</span><span class="sxs-lookup"><span data-stu-id="96d27-120">The **hive.auto.convert.join.noconditionaltask** in the hive-site.xml file was set to **true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="96d27-121">Il est probable que la jointure de carte a été la cause de l’erreur de mémoire insuffisante de l’espace de tas Java.</span><span class="sxs-lookup"><span data-stu-id="96d27-121">It is likely map join was the cause of the Java Heap Space our of memory error.</span></span> <span data-ttu-id="96d27-122">Comme expliqué dans le billet de blog [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), lorsque le moteur d’exécution Tez est utilisé, l’espace de tas utilisé appartient en fait au conteneur Tez.</span><span class="sxs-lookup"><span data-stu-id="96d27-122">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="96d27-123">Consultez l’image suivante décrivant la mémoire de conteneur Tez.</span><span class="sxs-lookup"><span data-stu-id="96d27-123">See the following image describing the Tez container memory.</span></span>

![Diagramme de la mémoire du conteneur Tez : erreur de mémoire insuffisante dans Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="96d27-125">Comme le suggère le billet de blog, les deux paramètres de mémoire suivants définissent la mémoire de conteneur du tas : **hive.tez.container.size** et **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="96d27-125">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="96d27-126">D’après notre expérience, l’exception relative à une mémoire insuffisante ne signifie pas que la taille du conteneur est trop petite.</span><span class="sxs-lookup"><span data-stu-id="96d27-126">From our experience, the out of memory exception does not mean the container size is too small.</span></span> <span data-ttu-id="96d27-127">Elle signifie que la taille du tas Java (hive.tez.java.opts) est trop petite.</span><span class="sxs-lookup"><span data-stu-id="96d27-127">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="96d27-128">Par conséquent, lorsque vous voyez une erreur de mémoire insuffisante, vous pouvez essayer d’augmenter la valeur de **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="96d27-128">So whenever you see out of memory, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="96d27-129">Si nécessaire, vous pouvez augmenter **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="96d27-129">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="96d27-130">Le paramètre **java.opts** doit correspondre à environ 80 % de la taille de conteneur (**container.size**).</span><span class="sxs-lookup"><span data-stu-id="96d27-130">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="96d27-131">Le paramètre **hive.tez.java.opts** doit toujours être inférieur à **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="96d27-131">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="96d27-132">Comme un ordinateur D12 a une mémoire de 28 Go, nous avons décidé d’utiliser une taille de conteneur de 10 Go (10 240 Mo) et d’affecter la valeur 80 % à java.opts :</span><span class="sxs-lookup"><span data-stu-id="96d27-132">Because a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="96d27-133">Avec les nouveaux paramètres, la requête s’est correctement exécutée en moins de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="96d27-133">With the new settings, the query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96d27-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="96d27-134">Next steps</span></span>

<span data-ttu-id="96d27-135">L’obtention d’une erreur de mémoire insuffisante ne signifie pas nécessairement que la taille du conteneur est insuffisante.</span><span class="sxs-lookup"><span data-stu-id="96d27-135">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="96d27-136">Vous devez plutôt configurer les paramètres de mémoire afin que la taille du tas soit augmentée et qu’elle représente au moins 80 % de la taille de la mémoire du conteneur.</span><span class="sxs-lookup"><span data-stu-id="96d27-136">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span> <span data-ttu-id="96d27-137">Pour optimiser les requêtes Hive, consultez [Optimisation des requêtes Hive pour Hadoop dans HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="96d27-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>