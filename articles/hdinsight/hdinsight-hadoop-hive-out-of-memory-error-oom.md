---
title: "aaaFix une ruche de l’erreur de mémoire dans Azure HDInsight | Documents Microsoft"
description: "Corrigez une erreur de mémoire insuffisante Hive dans Azure HDInsight. scénario de client Hello est une requête sur plusieurs tables de grande taille."
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
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="60450-105">Corriger une erreur de mémoire insuffisante Hive dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="60450-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="60450-106">Découvrez comment toofix une ruche : erreur de mémoire insuffisante lorsque traitez des tables volumineuses en configurant les paramètres de mémoire Hive.</span><span class="sxs-lookup"><span data-stu-id="60450-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="60450-107">Exécuter une requête Hive sur des tables de grande taille</span><span class="sxs-lookup"><span data-stu-id="60450-107">Run Hive query against large tables</span></span>

<span data-ttu-id="60450-108">Un client exécute une requête Hive :</span><span class="sxs-lookup"><span data-stu-id="60450-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="60450-109">Voici quelques caractéristiques de cette requête :</span><span class="sxs-lookup"><span data-stu-id="60450-109">Some nuances of this query:</span></span>

* <span data-ttu-id="60450-110">T1 est une table big tooa alias, TABLE1, qui possède un grand nombre de types de colonnes de chaîne.</span><span class="sxs-lookup"><span data-stu-id="60450-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="60450-111">Les autres tables ne sont pas si volumineuses, mais elles ont un grand nombre de colonnes.</span><span class="sxs-lookup"><span data-stu-id="60450-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="60450-112">Toutes les tables sont associées les unes aux autres, parfois avec plusieurs colonnes dans TABLE1 et d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="60450-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="60450-113">requête Hive de Hello a pris 26 minutes toofinish sur un cluster de A3 HDInsight 24 nœud.</span><span class="sxs-lookup"><span data-stu-id="60450-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="60450-114">Hello client remarqué hello suivant des messages d’avertissement :</span><span class="sxs-lookup"><span data-stu-id="60450-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="60450-115">En utilisant le moteur d’exécution Tez hello.</span><span class="sxs-lookup"><span data-stu-id="60450-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="60450-116">Hello même requête exécuté pendant 15 minutes, puis a levé hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="60450-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="60450-117">Erreur de Hello reste lors de l’utilisation d’une machine virtuelle plus grande (par exemple, D12).</span><span class="sxs-lookup"><span data-stu-id="60450-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="60450-118">Déboguer hello erreur de mémoire insuffisante</span><span class="sxs-lookup"><span data-stu-id="60450-118">Debug hello out of memory error</span></span>

<span data-ttu-id="60450-119">La prise en charge et les équipes d’ingénierie ensemble trouvent à un des problèmes de hello à l’origine de hello erreur de mémoire insuffisante a été un [problème décrit dans hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="60450-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="60450-120">Hello **hive.auto.convert.join.noconditionaltask** dans hello hive-site.XML fichier a été défini trop**true**:</span><span class="sxs-lookup"><span data-stu-id="60450-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="60450-121">Il est probable que jointure de la carte a été provoqué hello hello espace du tas de Java notre erreur de mémoire.</span><span class="sxs-lookup"><span data-stu-id="60450-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="60450-122">Comme expliqué dans le billet de blog hello [les paramètres de mémoire fils de Hadoop dans HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), lorsque Tez moteur d’exécution est l’espace de tas de hello utilisé utilisé appartient réellement toohello Tez conteneur.</span><span class="sxs-lookup"><span data-stu-id="60450-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="60450-123">Consultez hello suivant de la mémoire image décrivant hello Tez conteneur.</span><span class="sxs-lookup"><span data-stu-id="60450-123">See hello following image describing hello Tez container memory.</span></span>

![Diagramme de la mémoire du conteneur Tez : erreur de mémoire insuffisante dans Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="60450-125">Comme l’indique, billet de blog hello hello suivant deux paramètres de mémoire définir la mémoire de conteneur de hello pour le segment de mémoire hello : **hive.tez.container.size** et **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="60450-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="60450-126">À partir de notre expérience, hello à l’exception de mémoire insuffisante ne signifie pas conteneur hello est trop petite.</span><span class="sxs-lookup"><span data-stu-id="60450-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="60450-127">Cela signifie hello taille du tas de Java (hive.tez.java.opts) est trop petite.</span><span class="sxs-lookup"><span data-stu-id="60450-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="60450-128">Chaque fois que vous voyez la mémoire, vous pouvez effectuer tooincrease **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="60450-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="60450-129">Si nécessaire avoir tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="60450-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="60450-130">Hello **java.opts** paramètre doit être environ 80 % de **container.size**.</span><span class="sxs-lookup"><span data-stu-id="60450-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="60450-131">paramètre de Hello **hive.tez.java.opts** doit toujours être inférieur à **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="60450-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="60450-132">Un ordinateur D12 ayant 28 Go de mémoire, nous décidé toouse une taille de conteneur de 10 Go (10240 Mo) et affecter 80 % toojava.opts :</span><span class="sxs-lookup"><span data-stu-id="60450-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="60450-133">Avec les nouveaux paramètres de hello, l’exécution de requête de hello correctement dans moins de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="60450-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60450-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60450-134">Next steps</span></span>

<span data-ttu-id="60450-135">Une erreur d’insuffisance de mémoire ne signifie pas nécessairement conteneur hello est trop petite.</span><span class="sxs-lookup"><span data-stu-id="60450-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="60450-136">Au lieu de cela, vous devez configurer les paramètres de mémoire hello afin que la taille du tas hello est augmentée et au moins 80 % de la taille de la mémoire hello conteneur.</span><span class="sxs-lookup"><span data-stu-id="60450-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="60450-137">Pour optimiser les requêtes Hive, consultez [Optimisation des requêtes Hive pour Hadoop dans HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="60450-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
