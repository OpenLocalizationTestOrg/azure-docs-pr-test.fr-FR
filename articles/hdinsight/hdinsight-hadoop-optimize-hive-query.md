---
title: "aaaOptimize ruche les requêtes dans Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toooptimize votre ruche interroge pour Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="81d17-103">Optimisation des requêtes Hive dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="81d17-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="81d17-104">Par défaut, les clusters Hadoop ne sont pas optimisés pour les performances.</span><span class="sxs-lookup"><span data-stu-id="81d17-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="81d17-105">Cet article traite de certaines méthodes de l’optimisation de performances ruche plus courantes que vous pouvez appliquer des requêtes tooyour.</span><span class="sxs-lookup"><span data-stu-id="81d17-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="81d17-106">Montée en charge des nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="81d17-106">Scale out worker nodes</span></span>

<span data-ttu-id="81d17-107">Augmentation du nombre hello de nœuds de travail dans un cluster peut exploiter plus toobe REDUCTEURS et des mappeurs de s’exécuter en parallèle.</span><span class="sxs-lookup"><span data-stu-id="81d17-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="81d17-108">Il existe deux manières d’accroître la montée en charge dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="81d17-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="81d17-109">Au moment de configurer hello, vous pouvez spécifier le nombre hello de nœuds de travail à l’aide de hello portail Azure, Azure PowerShell ou une interface de ligne inter-plateformes.</span><span class="sxs-lookup"><span data-stu-id="81d17-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="81d17-110">Pour plus d’informations, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="81d17-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="81d17-111">Hello capture d’écran suivante montre les processus de travail hello configuration du nœud sur hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="81d17-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="81d17-113">Au moment de l’exécution de hello, vous pouvez également monter en charge un cluster sans avoir à recréer un :</span><span class="sxs-lookup"><span data-stu-id="81d17-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="81d17-115">Pour plus d’informations sur les différentes machines virtuelles hello, pris en charge par HDInsight, consultez [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="81d17-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="81d17-116">Activation de Tez</span><span class="sxs-lookup"><span data-stu-id="81d17-116">Enable Tez</span></span>

<span data-ttu-id="81d17-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) est un moteur de remplacement de l’exécution du moteur toohello MapReduce :</span><span class="sxs-lookup"><span data-stu-id="81d17-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="81d17-119">Tez est plus rapide pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="81d17-119">Tez is faster because:</span></span>

* <span data-ttu-id="81d17-120">**Exécutez graphique acyclique dirigé (DAG) en tant qu’une seule tâche dans le moteur de MapReduce hello**.</span><span class="sxs-lookup"><span data-stu-id="81d17-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="81d17-121">Hello DAG nécessite chaque ensemble de toobe mappeurs suivi d’un ensemble de REDUCTEURS.</span><span class="sxs-lookup"><span data-stu-id="81d17-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="81d17-122">Cela entraîne plusieurs toobe de travaux MapReduce tourné pour chaque requête Hive.</span><span class="sxs-lookup"><span data-stu-id="81d17-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="81d17-123">Tez n’a pas de telles contraintes et peut traiter un graphique orienté acyclique comme une tâche unique, ce qui réduit la surcharge de démarrage de tâche.</span><span class="sxs-lookup"><span data-stu-id="81d17-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="81d17-124">**Il évite les écritures inutiles**.</span><span class="sxs-lookup"><span data-stu-id="81d17-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="81d17-125">En raison de travaux toomultiple est tourné pour hello même requête Hive dans le moteur MapReduce hello, sortie hello de chaque travail est écrit tooHDFS pour les données intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="81d17-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="81d17-126">Étant donné que Tez réduit le nombre de tâches pour chaque requête Hive qu'il est en mesure de tooavoid inutiles en écriture.</span><span class="sxs-lookup"><span data-stu-id="81d17-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="81d17-127">**Il réduit les délais de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="81d17-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="81d17-128">Tez est le délai de démarrage toominimize en mesure de mieux en réduisant le nombre hello de mappeurs, qu'il doit toostart et également améliorer l’optimisation dans l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="81d17-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="81d17-129">**Il réutilise les conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="81d17-129">**Reuses containers**.</span></span> <span data-ttu-id="81d17-130">Chaque fois que Tez possible est que la latence en raison de tooreuse en mesure de conteneurs tooensure toostarting des conteneurs est réduite.</span><span class="sxs-lookup"><span data-stu-id="81d17-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="81d17-131">**Il utilise des techniques d’optimisation continue**.</span><span class="sxs-lookup"><span data-stu-id="81d17-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="81d17-132">Généralement, l’optimisation est effectuée lors de la compilation.</span><span class="sxs-lookup"><span data-stu-id="81d17-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="81d17-133">Toutefois, vous trouverez plus d’informations sur les entrées de hello qui permettent une meilleure optimisation pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="81d17-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="81d17-134">Tez utilise des techniques d’optimisation continue qui lui permet de plan de hello toooptimize davantage en phase d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="81d17-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="81d17-135">Pour plus d’informations sur ces concepts, consultez [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="81d17-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="81d17-136">Vous pouvez choisir n’importe quelle requête Hive Tez activé en attribuant un requête de hello paramètre hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="81d17-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="81d17-137">Tez est activé par défaut pour les clusters HDInsight basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="81d17-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="81d17-138">Partitionnement Hive</span><span class="sxs-lookup"><span data-stu-id="81d17-138">Hive partitioning</span></span>

<span data-ttu-id="81d17-139">L’opération d’e/s est goulot d’étranglement de performances hello pour l’exécution de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="81d17-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="81d17-140">performances de Hello peuvent être améliorées si quantité hello de données toobe lecture peut être réduite.</span><span class="sxs-lookup"><span data-stu-id="81d17-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="81d17-141">Par défaut, les requêtes Hive analysent l’ensemble des tables Hive.</span><span class="sxs-lookup"><span data-stu-id="81d17-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="81d17-142">Cela est très utile pour les requêtes telles que les analyses de tables.</span><span class="sxs-lookup"><span data-stu-id="81d17-142">This is great for queries like table scans.</span></span> <span data-ttu-id="81d17-143">Toutefois pour les requêtes qui doivent uniquement tooscan une petite quantité de données (par exemple, les requêtes avec un filtrage), ce comportement crée inutile surcharge.</span><span class="sxs-lookup"><span data-stu-id="81d17-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="81d17-144">Partitionnement de la ruche permet de ruche requêtes tooaccess uniquement hello quantité de données dans les tables de la ruche.</span><span class="sxs-lookup"><span data-stu-id="81d17-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="81d17-145">Partitionnement de la ruche est implémenté par la réorganisation des données brutes hello dans nouveaux répertoires avec chaque partition ayant son propre répertoire - où la partition de hello est définie par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="81d17-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="81d17-146">Hello diagramme suivant illustre une table Hive le partitionnement par colonne de hello *année*.</span><span class="sxs-lookup"><span data-stu-id="81d17-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="81d17-147">Un nouveau répertoire est créé pour chaque année.</span><span class="sxs-lookup"><span data-stu-id="81d17-147">A new directory is created for each year.</span></span>

![partitionnement][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="81d17-149">Considérations relatives au partitionnement :</span><span class="sxs-lookup"><span data-stu-id="81d17-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="81d17-150">**Évitez les sous-partitionnements** : les partitionnements appliqués à des colonnes contenant uniquement quelques valeurs peuvent entraîner quelques partitions.</span><span class="sxs-lookup"><span data-stu-id="81d17-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="81d17-151">Par exemple, partitionnement sexe crée uniquement de deux partitions toobe créé (hommes et femmes), donc uniquement réduire la latence de hello en un maximum de moitié.</span><span class="sxs-lookup"><span data-stu-id="81d17-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="81d17-152">**Pas sur la partition** - dans hello inverse, si vous créez une partition sur une colonne avec une valeur unique (par exemple, userid), plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="81d17-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="81d17-153">Sur la partition entraîne de stress sur hello cluster namenode car elle a toohandle hello grand nombre de répertoires.</span><span class="sxs-lookup"><span data-stu-id="81d17-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="81d17-154">**Évitez le décalage de données** : choisissez votre clé de partitionnement avec soin, pour que toutes les partitions soient de taille égale.</span><span class="sxs-lookup"><span data-stu-id="81d17-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="81d17-155">Un exemple est le partitionnement sur *état* peut entraîner le nombre de hello d’enregistrements sous Californie toobe presque 30 x qui du Vermont en raison de la différence de toohello de remplissage.</span><span class="sxs-lookup"><span data-stu-id="81d17-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="81d17-156">toocreate une table de partition, utilisez hello *partitionnée par* clause :</span><span class="sxs-lookup"><span data-stu-id="81d17-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="81d17-157">Après la création de la table partitionnée de hello, vous pouvez créer un partitionnement statique ou le partitionnement dynamique.</span><span class="sxs-lookup"><span data-stu-id="81d17-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="81d17-158">**Partitionnement statique** signifie que les données déjà partitionnées Bonjour les répertoires adéquats et vous pouvez demander des partitions de ruche manuellement basées sur l’emplacement du répertoire hello.</span><span class="sxs-lookup"><span data-stu-id="81d17-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="81d17-159">Hello suivant extrait de code est un exemple.</span><span class="sxs-lookup"><span data-stu-id="81d17-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="81d17-160">**Le partitionnement dynamique** signifie que vous voulez ruche toocreate partitions automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="81d17-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="81d17-161">Étant donné que nous avons déjà créé hello partitionnement de table à partir de la table intermédiaire de hello, il suffit de toodo est table toohello partitionnée de données insert :</span><span class="sxs-lookup"><span data-stu-id="81d17-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="81d17-162">Pour plus d’informations, consultez [Tables partitionnées](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="81d17-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="81d17-163">Utilisez le format ORCFile hello</span><span class="sxs-lookup"><span data-stu-id="81d17-163">Use hello ORCFile format</span></span>
<span data-ttu-id="81d17-164">Hive prend en charge différents formats de fichier.</span><span class="sxs-lookup"><span data-stu-id="81d17-164">Hive supports different file formats.</span></span> <span data-ttu-id="81d17-165">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="81d17-165">For example:</span></span>

* <span data-ttu-id="81d17-166">**Texte**: il s’agit du format de fichier par défaut hello et fonctionne avec la plupart des scénarios</span><span class="sxs-lookup"><span data-stu-id="81d17-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="81d17-167">**Avro**: fonctionne correctement avec les scénarios d’interopérabilité</span><span class="sxs-lookup"><span data-stu-id="81d17-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="81d17-168">**ORC/Parquet**: adapté pour les performances</span><span class="sxs-lookup"><span data-stu-id="81d17-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="81d17-169">Format ORC (optimisée en ligne en colonnes) est un toostore hautement efficace des données de ruche.</span><span class="sxs-lookup"><span data-stu-id="81d17-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="81d17-170">Formats tooother comparés, ORC a hello suivant avantages :</span><span class="sxs-lookup"><span data-stu-id="81d17-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="81d17-171">prise en charge des types complexes, notamment les types DateTime, ainsi que les types semi-structurés ;</span><span class="sxs-lookup"><span data-stu-id="81d17-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="81d17-172">la compression de too70 %</span><span class="sxs-lookup"><span data-stu-id="81d17-172">up too70% compression</span></span>
* <span data-ttu-id="81d17-173">création d’index toutes les 10 000 lignes, ce qui permet d’ignorer des lignes ;</span><span class="sxs-lookup"><span data-stu-id="81d17-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="81d17-174">baisse significative de l’exécution du démarrage.</span><span class="sxs-lookup"><span data-stu-id="81d17-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="81d17-175">format ORC tooenable, vous créez une table avec la clause de hello *stockés en tant que ORC*:</span><span class="sxs-lookup"><span data-stu-id="81d17-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="81d17-176">Vous insérez ensuite la table de données toohello ORC à partir de la table intermédiaire de hello.</span><span class="sxs-lookup"><span data-stu-id="81d17-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="81d17-177">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="81d17-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="81d17-178">Vous pouvez en savoir plus sur le format ORC hello [ici](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="81d17-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="81d17-179">Vectorisation</span><span class="sxs-lookup"><span data-stu-id="81d17-179">Vectorization</span></span>

<span data-ttu-id="81d17-180">Vectorisation permet la ruche tooprocess un lot de 1024 lignes ensemble au lieu de traiter une ligne à la fois.</span><span class="sxs-lookup"><span data-stu-id="81d17-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="81d17-181">Cela signifie que des opérations simples sont effectuées plus rapidement car toorun a besoin de moins de code interne.</span><span class="sxs-lookup"><span data-stu-id="81d17-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="81d17-182">tooenable vectorisation préfixe votre requête Hive avec hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="81d17-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="81d17-183">Pour plus d’informations, consultez la page [Exécution de requêtes vectorisées](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="81d17-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="81d17-184">Autres méthodes d’optimisation</span><span class="sxs-lookup"><span data-stu-id="81d17-184">Other optimization methods</span></span>
<span data-ttu-id="81d17-185">Vous pouvez envisager plusieurs autres méthodes d’optimisation, par exemple :</span><span class="sxs-lookup"><span data-stu-id="81d17-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="81d17-186">**La ruche de création de compartiments :** une technique qui permet de toocluster ou segment de grands jeux de données toooptimize des performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="81d17-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="81d17-187">**L’optimisation de jointure :** l’optimisation de l’exécution de requêtes de la ruche du planning tooimprove hello l’efficacité de jointures et réduire les besoins de hello pour les indicateurs de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81d17-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="81d17-188">Pour plus d’informations, consultez la page [Optimisation des jointures](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="81d17-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="81d17-189">**Augmentez les raccords de réduction**.</span><span class="sxs-lookup"><span data-stu-id="81d17-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81d17-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81d17-190">Next steps</span></span>
<span data-ttu-id="81d17-191">Dans cet article, vous avez appris plusieurs méthodes d’optimisation courantes des requêtes.</span><span class="sxs-lookup"><span data-stu-id="81d17-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="81d17-192">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="81d17-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="81d17-193">Utilisation d’Apache Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="81d17-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="81d17-194">Analyse des données sur les retards de vol avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="81d17-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="81d17-195">Analyse des données Twitter avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="81d17-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="81d17-196">Analyser les données de capteur à l’aide de hello Console de requête Hive sur Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="81d17-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="81d17-197">Utilisez la ruche avec des journaux de tooanalyze HDInsight à partir de sites Web</span><span class="sxs-lookup"><span data-stu-id="81d17-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
