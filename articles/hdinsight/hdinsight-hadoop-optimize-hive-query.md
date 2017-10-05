---
title: "Optimisation des requêtes Hive dans Azure HDInsight | Microsoft Docs"
description: "Apprenez à optimiser vos requêtes pour Hadoop dans HDInsight"
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
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="c96d8-103">Optimisation des requêtes Hive dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c96d8-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="c96d8-104">Par défaut, les clusters Hadoop ne sont pas optimisés pour les performances.</span><span class="sxs-lookup"><span data-stu-id="c96d8-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="c96d8-105">Cet article présente quelques-unes des méthodes d’optimisation des performances Hive courantes que vous pouvez appliquer à nos requêtes.</span><span class="sxs-lookup"><span data-stu-id="c96d8-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="c96d8-106">Montée en charge des nœuds de travail</span><span class="sxs-lookup"><span data-stu-id="c96d8-106">Scale out worker nodes</span></span>

<span data-ttu-id="c96d8-107">L’augmentation du nombre de nœuds de travail d’un cluster permet d’exploiter l’exécution de mappeurs et de raccords de réduction en parallèle.</span><span class="sxs-lookup"><span data-stu-id="c96d8-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="c96d8-108">Il existe deux manières d’accroître la montée en charge dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c96d8-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="c96d8-109">Au moment de l’approvisionnement, vous pouvez spécifier le nombre de nœuds Worker à l’aide du portail Azure, d’Azure PowerShell ou d’une interface de ligne de commande multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="c96d8-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="c96d8-110">Pour plus d’informations, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c96d8-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="c96d8-111">La capture d’écran suivante montre la configuration du nœud Worker sur le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="c96d8-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="c96d8-113">Au moment de l’exécution, vous pouvez également monter en charge un cluster sans en recréer un autre :</span><span class="sxs-lookup"><span data-stu-id="c96d8-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="c96d8-115">Pour plus d’informations sur les différentes machines virtuelles prises en charge par HDInsight, consultez la [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c96d8-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="c96d8-116">Activation de Tez</span><span class="sxs-lookup"><span data-stu-id="c96d8-116">Enable Tez</span></span>

<span data-ttu-id="c96d8-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) est un moteur d’exécution représentant une alternative au moteur MapReduce :</span><span class="sxs-lookup"><span data-stu-id="c96d8-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="c96d8-119">Tez est plus rapide pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="c96d8-119">Tez is faster because:</span></span>

* <span data-ttu-id="c96d8-120">**Il exécute un graphe orienté acyclique (DAG) en tant que tâche unique dans le moteur MapReduce**.</span><span class="sxs-lookup"><span data-stu-id="c96d8-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="c96d8-121">Le DAG requiert que chaque ensemble de mappeurs soit suivi par un ensemble de raccords de réduction.</span><span class="sxs-lookup"><span data-stu-id="c96d8-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="c96d8-122">Cela provoque la préparation de plusieurs tâches MapReduce pour chaque requête Hive.</span><span class="sxs-lookup"><span data-stu-id="c96d8-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="c96d8-123">Tez n’a pas de telles contraintes et peut traiter un graphique orienté acyclique comme une tâche unique, ce qui réduit la surcharge de démarrage de tâche.</span><span class="sxs-lookup"><span data-stu-id="c96d8-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="c96d8-124">**Il évite les écritures inutiles**.</span><span class="sxs-lookup"><span data-stu-id="c96d8-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="c96d8-125">Lorsque plusieurs tâches sont préparées pour la même requête Hive dans le moteur MapReduce, la sortie de chacune d’elles est écrite vers HDFS pour les données intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="c96d8-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="c96d8-126">Comme Tez réduit le nombre de tâches de chaque requête Hive, il est possible d’éviter de telles écritures inutiles.</span><span class="sxs-lookup"><span data-stu-id="c96d8-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="c96d8-127">**Il réduit les délais de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="c96d8-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="c96d8-128">Tez peut réduire davantage le délai de démarrage en réduisant le nombre de mappeurs nécessaires au démarrage tout en améliorant l’optimisation tout au long du processus.</span><span class="sxs-lookup"><span data-stu-id="c96d8-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="c96d8-129">**Il réutilise les conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="c96d8-129">**Reuses containers**.</span></span> <span data-ttu-id="c96d8-130">Dès que possible, Tez peut réutiliser les conteneurs pour réduire la latence provoquée par le nombre de conteneurs au démarrage.</span><span class="sxs-lookup"><span data-stu-id="c96d8-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="c96d8-131">**Il utilise des techniques d’optimisation continue**.</span><span class="sxs-lookup"><span data-stu-id="c96d8-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="c96d8-132">Généralement, l’optimisation est effectuée lors de la compilation.</span><span class="sxs-lookup"><span data-stu-id="c96d8-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="c96d8-133">Cependant, des informations supplémentaires sur les entrées sont disponibles pour améliorer l’optimisation durant le démarrage.</span><span class="sxs-lookup"><span data-stu-id="c96d8-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="c96d8-134">Tez utilise des techniques d’optimisation continue permettant d’améliorer le plan lors du démarrage.</span><span class="sxs-lookup"><span data-stu-id="c96d8-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="c96d8-135">Pour plus d’informations sur ces concepts, consultez [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="c96d8-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="c96d8-136">Vous pouvez activer n’importe quelle requête Hive pour Tez en faisant précéder la requête du paramètre ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c96d8-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="c96d8-137">Tez est activé par défaut pour les clusters HDInsight basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="c96d8-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="c96d8-138">Partitionnement Hive</span><span class="sxs-lookup"><span data-stu-id="c96d8-138">Hive partitioning</span></span>

<span data-ttu-id="c96d8-139">Les opérations d’E/S constituent le principal goulot d’étranglement des performances pour l’exécution de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="c96d8-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="c96d8-140">Il est possible d’améliorer les performances en réduisant la quantité de données à lire.</span><span class="sxs-lookup"><span data-stu-id="c96d8-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="c96d8-141">Par défaut, les requêtes Hive analysent l’ensemble des tables Hive.</span><span class="sxs-lookup"><span data-stu-id="c96d8-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="c96d8-142">Cela est très utile pour les requêtes telles que les analyses de tables.</span><span class="sxs-lookup"><span data-stu-id="c96d8-142">This is great for queries like table scans.</span></span> <span data-ttu-id="c96d8-143">Cependant, ce comportement crée une surcharge inutile pour les requêtes analysant seulement une petite quantité de données (par exemple, les requêtes avec filtrage).</span><span class="sxs-lookup"><span data-stu-id="c96d8-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="c96d8-144">Le partitionnement Hive permet aux requêtes Hive d’accéder uniquement à la quantité de données nécessaire dans les tables Hive.</span><span class="sxs-lookup"><span data-stu-id="c96d8-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="c96d8-145">Le partitionnement Hive est implémenté en réorganisant les données brutes en nouveaux répertoires où chaque partition a son propre répertoire, comme défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c96d8-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="c96d8-146">Le schéma suivant illustre le partitionnement d’une table Hive selon la colonne *Année*.</span><span class="sxs-lookup"><span data-stu-id="c96d8-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="c96d8-147">Un nouveau répertoire est créé pour chaque année.</span><span class="sxs-lookup"><span data-stu-id="c96d8-147">A new directory is created for each year.</span></span>

![partitionnement][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="c96d8-149">Considérations relatives au partitionnement :</span><span class="sxs-lookup"><span data-stu-id="c96d8-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="c96d8-150">**Évitez les sous-partitionnements** : les partitionnements appliqués à des colonnes contenant uniquement quelques valeurs peuvent entraîner quelques partitions.</span><span class="sxs-lookup"><span data-stu-id="c96d8-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="c96d8-151">Par exemple, un partitionnement de genre crée uniquement deux partitions (masculin et féminin), ce qui réduit la latence de moitié seulement.</span><span class="sxs-lookup"><span data-stu-id="c96d8-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="c96d8-152">**Évitez les sur-partitionnements** : l’autre extrême, le partitionnement appliqué à une colonne avec une valeur unique (par exemple, userid) entraîne de nombreuses partitions.</span><span class="sxs-lookup"><span data-stu-id="c96d8-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="c96d8-153">Le sur-partitionnement communique un stress important au cluster namenode, car ce dernier doit gérer de grandes quantités de répertoires.</span><span class="sxs-lookup"><span data-stu-id="c96d8-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="c96d8-154">**Évitez le décalage de données** : choisissez votre clé de partitionnement avec soin, pour que toutes les partitions soient de taille égale.</span><span class="sxs-lookup"><span data-stu-id="c96d8-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="c96d8-155">Par exemple, le partitionnement sur *Région* peut entraîner un nombre d’enregistrements sous Île-de-France 30 fois supérieur à celui sous Franche-Comté, en raison de la différence de population.</span><span class="sxs-lookup"><span data-stu-id="c96d8-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="c96d8-156">Pour créer une table de partition, utilisez la clause *Partitioned By* :</span><span class="sxs-lookup"><span data-stu-id="c96d8-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="c96d8-157">Lorsque la table partitionnée est créée, vous pouvez créer un partitionnement statique ou dynamique.</span><span class="sxs-lookup"><span data-stu-id="c96d8-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="c96d8-158">**Partitionnement statique** signifie que vous avez déjà partagé des données dans des répertoires appropriés et que vous pouvez demander des partitions Hive manuellement en fonction de l’emplacement du répertoire.</span><span class="sxs-lookup"><span data-stu-id="c96d8-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="c96d8-159">L’extrait de code suivant est un exemple.</span><span class="sxs-lookup"><span data-stu-id="c96d8-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="c96d8-160">**Partitionnement dynamique** signifie que vous voulez que Hive crée automatiquement des partitions pour vous.</span><span class="sxs-lookup"><span data-stu-id="c96d8-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="c96d8-161">Étant donné que nous avons déjà créé la table de partitionnement à partir de la table intermédiaire, il nous suffit d’insérer des données dans la table partitionnée :</span><span class="sxs-lookup"><span data-stu-id="c96d8-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="c96d8-162">Pour plus d’informations, consultez [Tables partitionnées](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="c96d8-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="c96d8-163">Utilisation du format ORCFile</span><span class="sxs-lookup"><span data-stu-id="c96d8-163">Use the ORCFile format</span></span>
<span data-ttu-id="c96d8-164">Hive prend en charge différents formats de fichier.</span><span class="sxs-lookup"><span data-stu-id="c96d8-164">Hive supports different file formats.</span></span> <span data-ttu-id="c96d8-165">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c96d8-165">For example:</span></span>

* <span data-ttu-id="c96d8-166">**Texte**: il s’agit du format de fichier par défaut, qui fonctionne avec la plupart des scénarios</span><span class="sxs-lookup"><span data-stu-id="c96d8-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="c96d8-167">**Avro**: fonctionne correctement avec les scénarios d’interopérabilité</span><span class="sxs-lookup"><span data-stu-id="c96d8-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="c96d8-168">**ORC/Parquet**: adapté pour les performances</span><span class="sxs-lookup"><span data-stu-id="c96d8-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="c96d8-169">Le format ORC (Optimized Row Columnar) est un moyen très efficace pour stocker des données Hive.</span><span class="sxs-lookup"><span data-stu-id="c96d8-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="c96d8-170">Par rapport aux autres formats, ORC présente les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c96d8-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="c96d8-171">prise en charge des types complexes, notamment les types DateTime, ainsi que les types semi-structurés ;</span><span class="sxs-lookup"><span data-stu-id="c96d8-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="c96d8-172">jusqu’à 70 % de compression ;</span><span class="sxs-lookup"><span data-stu-id="c96d8-172">up to 70% compression</span></span>
* <span data-ttu-id="c96d8-173">création d’index toutes les 10 000 lignes, ce qui permet d’ignorer des lignes ;</span><span class="sxs-lookup"><span data-stu-id="c96d8-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="c96d8-174">baisse significative de l’exécution du démarrage.</span><span class="sxs-lookup"><span data-stu-id="c96d8-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="c96d8-175">Pour activer le format ORC, vous devez commencer par créer une table avec la clause *Stored as ORC*:</span><span class="sxs-lookup"><span data-stu-id="c96d8-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="c96d8-176">Ensuite, vous devez insérer des données dans la table ORC à partir de la table de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="c96d8-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="c96d8-177">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c96d8-177">For example:</span></span>

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

<span data-ttu-id="c96d8-178">Vous pouvez en savoir plus sur le format ORC [ici](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="c96d8-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="c96d8-179">Vectorisation</span><span class="sxs-lookup"><span data-stu-id="c96d8-179">Vectorization</span></span>

<span data-ttu-id="c96d8-180">La vectorisation permet à Hive de traiter un lot de 1024 lignes simultanément, au lieu d’une ligne à la fois.</span><span class="sxs-lookup"><span data-stu-id="c96d8-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="c96d8-181">Cela signifie que les opérations simples sont effectuées plus rapidement, car elles requièrent moins d’exécution de code interne.</span><span class="sxs-lookup"><span data-stu-id="c96d8-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="c96d8-182">Pour activer la vectorisation, faites précéder vos requêtes Hive par le paramètre suivant :</span><span class="sxs-lookup"><span data-stu-id="c96d8-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="c96d8-183">Pour plus d’informations, consultez la page [Exécution de requêtes vectorisées](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="c96d8-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="c96d8-184">Autres méthodes d’optimisation</span><span class="sxs-lookup"><span data-stu-id="c96d8-184">Other optimization methods</span></span>
<span data-ttu-id="c96d8-185">Vous pouvez envisager plusieurs autres méthodes d’optimisation, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c96d8-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="c96d8-186">**Création de compartiments Hive** : cette technique permet de mettre en cluster ou de segmenter des jeux de données volumineux pour optimiser les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="c96d8-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="c96d8-187">**Optimisation des jointures** : une optimisation de la planification de l’exécution des requêtes Hive pour améliorer l’efficacité des jointures et réduire le besoin d’indicateurs utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c96d8-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="c96d8-188">Pour plus d’informations, consultez la page [Optimisation des jointures](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="c96d8-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="c96d8-189">**Augmentez les raccords de réduction**.</span><span class="sxs-lookup"><span data-stu-id="c96d8-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c96d8-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c96d8-190">Next steps</span></span>
<span data-ttu-id="c96d8-191">Dans cet article, vous avez appris plusieurs méthodes d’optimisation courantes des requêtes.</span><span class="sxs-lookup"><span data-stu-id="c96d8-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="c96d8-192">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="c96d8-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="c96d8-193">Utilisation d’Apache Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c96d8-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c96d8-194">Analyse des données sur les retards de vol avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c96d8-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="c96d8-195">Analyse des données Twitter avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c96d8-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="c96d8-196">Analyse des données de capteur à l’aide de la console de requête Hive sur Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c96d8-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="c96d8-197">Utilisation de Hive avec HDInsight pour analyser les journaux de site web</span><span class="sxs-lookup"><span data-stu-id="c96d8-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
