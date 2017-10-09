---
title: aaaUse Beeline avec Apache Hive - Azure HDInsight | Documents Microsoft
description: "Découvrez le fonctionnement des requêtes toouse hello Beeline client toorun Hive avec Hadoop dans HDInsight. Beeline est un utilitaire qui permet d’utiliser HiveServer2 sur JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive,hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="19354-105">Utiliser le client de Beeline hello avec Apache Hive</span><span class="sxs-lookup"><span data-stu-id="19354-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="19354-106">Découvrez comment toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun ruche interroge sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="19354-107">Beeline est un client de la ruche qui est inclus dans les nœuds principaux d’hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="19354-108">Beeline utilise JDBC tooconnect tooHiveServer2, un service hébergé sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="19354-109">Vous pouvez également utiliser Beeline tooaccess Hive dans HDInsight à distance plus hello internet.</span><span class="sxs-lookup"><span data-stu-id="19354-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="19354-110">Hello tableau suivant fournit des chaînes de connexion pour une utilisation avec Beeline :</span><span class="sxs-lookup"><span data-stu-id="19354-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="19354-111">Emplacement d’exécution de Beeline</span><span class="sxs-lookup"><span data-stu-id="19354-111">Where you run Beeline from</span></span> | <span data-ttu-id="19354-112">Paramètres</span><span class="sxs-lookup"><span data-stu-id="19354-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19354-113">Un SSH tooa bord ou le nœud principal nœud de connexion</span><span class="sxs-lookup"><span data-stu-id="19354-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="19354-114">Cluster en dehors de hello</span><span class="sxs-lookup"><span data-stu-id="19354-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="19354-115">Remplacez `admin` avec un compte de connexion de cluster hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="19354-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="19354-116">Remplacez `password` avec mot de passe hello hello cluster compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="19354-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="19354-117">Remplacez `clustername` par nom de hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="19354-118"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="19354-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="19354-119">Un cluster Hadoop Linux sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="19354-120">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="19354-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19354-121">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="19354-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="19354-122">Un client SSH ou un client Beeline local.</span><span class="sxs-lookup"><span data-stu-id="19354-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="19354-123">La plupart des étapes hello dans ce document suppose que vous utilisez Beeline à partir d’un cluster de toohello session SSH.</span><span class="sxs-lookup"><span data-stu-id="19354-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="19354-124">Pour plus d’informations sur l’exécution de Beeline à partir du cluster en dehors de hello, consultez hello [utiliser Beeline à distance](#remote) section.</span><span class="sxs-lookup"><span data-stu-id="19354-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="19354-125">Pour plus d’informations sur l’utilisation de SSH, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="19354-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="19354-126"><a id="beeline"></a>Utiliser BeeLine</span><span class="sxs-lookup"><span data-stu-id="19354-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="19354-127">Lors du démarrage de Beeline, vous devez fournir une chaîne de connexion pour HiveServer2 sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="19354-128">commande hello de toorun du cluster de hello externe, vous devez également fournir le nom de compte de connexion de cluster hello (valeur par défaut `admin`) et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19354-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="19354-129">Utilisez hello suivant table toofind hello connexion chaîne format et les paramètres toouse :</span><span class="sxs-lookup"><span data-stu-id="19354-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="19354-130">Emplacement d’exécution de Beeline</span><span class="sxs-lookup"><span data-stu-id="19354-130">Where you run Beeline from</span></span> | <span data-ttu-id="19354-131">Paramètres</span><span class="sxs-lookup"><span data-stu-id="19354-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="19354-132">Un SSH tooa bord ou le nœud principal nœud de connexion</span><span class="sxs-lookup"><span data-stu-id="19354-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="19354-133">Cluster en dehors de hello</span><span class="sxs-lookup"><span data-stu-id="19354-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="19354-134">Par exemple, hello commande suivante peut être utilisé toostart Beeline à partir d’un cluster de toohello session SSH :</span><span class="sxs-lookup"><span data-stu-id="19354-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="19354-135">Cette commande démarre le client de Beeline hello et connecte tooHiveServer2 sur le nœud principal du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19354-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="19354-136">Une fois la commande hello terminée, vous accédez à un `jdbc:hive2://headnodehost:10001/>` invite.</span><span class="sxs-lookup"><span data-stu-id="19354-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="19354-137">Les commandes Beeline commencent par un caractère `!`. Par exemple, `!help` affiche l’aide.</span><span class="sxs-lookup"><span data-stu-id="19354-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="19354-138">Toutefois hello `!` peut être omis pour certaines commandes.</span><span class="sxs-lookup"><span data-stu-id="19354-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="19354-139">Par exemple, `help` fonctionne également.</span><span class="sxs-lookup"><span data-stu-id="19354-139">For example, `help` also works.</span></span>

    <span data-ttu-id="19354-140">Il existe un `!sql`, qui est utilisé tooexecute les instructions HiveQL.</span><span class="sxs-lookup"><span data-stu-id="19354-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="19354-141">Toutefois, HiveQL est couramment utilisé que vous pouvez omettre hello précédent `!sql`.</span><span class="sxs-lookup"><span data-stu-id="19354-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="19354-142">Hello suivant deux instructions est équivalente :</span><span class="sxs-lookup"><span data-stu-id="19354-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="19354-143">Sur un nouveau cluster, une seule table est listée : **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="19354-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="19354-144">Utilisez hello suivant schéma hello hello hivesampletable commande toodisplay :</span><span class="sxs-lookup"><span data-stu-id="19354-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="19354-145">Cette commande renvoie hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="19354-145">This command returns hello following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="19354-146">Cette section décrit les colonnes hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="19354-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="19354-147">Pendant que nous pouvons effectuer des requêtes sur ces données, nous allons plutôt créer un tout nouveau toodemonstrate de table comment les données de tooload dans la ruche et appliquer un schéma.</span><span class="sxs-lookup"><span data-stu-id="19354-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="19354-148">Entrez hello suivant les instructions toocreate une table nommée **log4jLogs** à l’aide des exemples de données fournis avec le cluster HDInsight de hello :</span><span class="sxs-lookup"><span data-stu-id="19354-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="19354-149">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="19354-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="19354-150">`DROP TABLE`-Si la table de hello existe, elle est supprimée.</span><span class="sxs-lookup"><span data-stu-id="19354-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="19354-151">`CREATE EXTERNAL TABLE` : crée une table **externe** dans Hive.</span><span class="sxs-lookup"><span data-stu-id="19354-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="19354-152">Les tables externes ne stockent la définition de table hello Hive.</span><span class="sxs-lookup"><span data-stu-id="19354-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="19354-153">les données de salutation reste dans l’emplacement d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="19354-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="19354-154">`ROW FORMAT`-Comment les données de salutation sont mis en forme.</span><span class="sxs-lookup"><span data-stu-id="19354-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="19354-155">Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="19354-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="19354-156">`STORED AS TEXTFILE LOCATION`-Emplacement de stockage des données de salutation et dans quel format de fichier.</span><span class="sxs-lookup"><span data-stu-id="19354-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="19354-157">`SELECT`-Sélectionne un nombre de toutes les lignes où colonne **t4** contient la valeur de hello **[erreur]**.</span><span class="sxs-lookup"><span data-stu-id="19354-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="19354-158">Cette requête renvoie la valeur **3**, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="19354-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="19354-159">`INPUT__FILE__NAME LIKE '%.log'`-Ruche tente de fichiers de tooall tooapply hello schéma dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="19354-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="19354-160">Dans ce cas, le répertoire de hello contient des fichiers qui ne correspondent pas hello schéma.</span><span class="sxs-lookup"><span data-stu-id="19354-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="19354-161">données de garbage tooprevent dans les résultats de hello, cette instruction indique ruche que nous devons retourner uniquement les données à partir de fichiers se terminant par. journal.</span><span class="sxs-lookup"><span data-stu-id="19354-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="19354-162">Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe.</span><span class="sxs-lookup"><span data-stu-id="19354-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="19354-163">Par exemple, un processus de chargement de données automatisé ou une opération MapReduce.</span><span class="sxs-lookup"><span data-stu-id="19354-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="19354-164">Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.</span><span class="sxs-lookup"><span data-stu-id="19354-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="19354-165">la sortie de cette commande est similaire toohello suivant texte Hello :</span><span class="sxs-lookup"><span data-stu-id="19354-165">hello output of this command is similar toohello following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="19354-166">tooexit Beeline, utilisez `!exit`.</span><span class="sxs-lookup"><span data-stu-id="19354-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="19354-167"><a id="file"></a>Utilisez Beeline toorun un fichier HiveQL</span><span class="sxs-lookup"><span data-stu-id="19354-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="19354-168">Utilisez hello suivant les étapes toocreate un fichier, puis l’exécuter à l’aide de Beeline.</span><span class="sxs-lookup"><span data-stu-id="19354-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="19354-169">Toocreate de commande suivant de hello d’utiliser un fichier nommé **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="19354-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="19354-170">Utilisez hello après le texte en tant que contenu hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="19354-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="19354-171">Cette requête crée une table « interne » nommée **errorLogs** :</span><span class="sxs-lookup"><span data-stu-id="19354-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="19354-172">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="19354-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="19354-173">**CREATE TABLE IF NOT EXISTS** -si la table de hello n’existe pas déjà, il est créé.</span><span class="sxs-lookup"><span data-stu-id="19354-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="19354-174">Depuis hello **externe** mot clé n’est pas utilisé, cette instruction crée une table interne.</span><span class="sxs-lookup"><span data-stu-id="19354-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="19354-175">Tables internes sont stockées dans l’entrepôt de données Hive hello et sont gérées entièrement par ruche.</span><span class="sxs-lookup"><span data-stu-id="19354-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="19354-176">**ORC de AS stockées** -stocke les données de hello dans format optimisé lignes en colonnes (ORC).</span><span class="sxs-lookup"><span data-stu-id="19354-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="19354-177">Le format ORC est particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="19354-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="19354-178">**INSERT OVERWRITE ... Sélectionnez** -sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des **[erreur]**, puis insère hello des données dans hello **journaux d’erreurs de** table.</span><span class="sxs-lookup"><span data-stu-id="19354-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19354-179">Contrairement aux tables externes, la suppression d’une table interne supprime également des données sous-jacentes hello.</span><span class="sxs-lookup"><span data-stu-id="19354-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="19354-180">fichier de hello toosave, utilisez **Ctrl**+**_X**, puis entrez **Y**et enfin **entrée**.</span><span class="sxs-lookup"><span data-stu-id="19354-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="19354-181">Utilisez hello toorun le fichier hello à l’aide de Beeline suivant :</span><span class="sxs-lookup"><span data-stu-id="19354-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="19354-182">Hello `-i` paramètre démarre Beeline, séries hello instructions hello query.hql fichier.</span><span class="sxs-lookup"><span data-stu-id="19354-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="19354-183">Une fois la requête de hello est terminée, vous arrivez à hello `jdbc:hive2://headnodehost:10001/>` invite.</span><span class="sxs-lookup"><span data-stu-id="19354-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="19354-184">Vous pouvez également exécuter un fichier à l’aide de hello `-f` paramètre, qui se termine Beeline une fois hello requête terminée.</span><span class="sxs-lookup"><span data-stu-id="19354-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="19354-185">tooverify hello **journaux d’erreurs** table a été créée, utilisez hello suivant tooreturn instruction tous hello des lignes à partir de **journaux d’erreurs de**:</span><span class="sxs-lookup"><span data-stu-id="19354-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="19354-186">Trois lignes de données doivent normalement être renvoyées. Elles contiennent toutes **[ERROR]** dans la colonne t4 :</span><span class="sxs-lookup"><span data-stu-id="19354-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="19354-187"><a id="remote"></a>Utiliser Beeline à distance</span><span class="sxs-lookup"><span data-stu-id="19354-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="19354-188">Si vous avez Beeline installé localement, ou que vous l’utilisez en via une image Docker comme [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), vous devez utiliser hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="19354-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="19354-189">__Chaîne de connexion__ : `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="19354-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="19354-190">__Nom de connexion du cluster__ : `-n admin`</span><span class="sxs-lookup"><span data-stu-id="19354-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="19354-191">__Mot de passe de connexion du cluster__ : `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="19354-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="19354-192">Remplacez hello `clustername` dans la chaîne de connexion hello nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="19354-193">Remplacez `admin` avec nom hello de votre connexion de cluster, puis remplacez `password` avec le mot de passe hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="19354-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="19354-194"><a id="sparksql"></a>Utilisez Beeline avec Spark</span><span class="sxs-lookup"><span data-stu-id="19354-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="19354-195">Spark fournit sa propre implémentation de HiveServer2, qui est souvent serveur Spark Thrift d’indiqué tooas hello.</span><span class="sxs-lookup"><span data-stu-id="19354-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="19354-196">Ce service utilise des requêtes de tooresolve Spark SQL au lieu de la ruche et peut offrir de meilleures performances en fonction de votre requête.</span><span class="sxs-lookup"><span data-stu-id="19354-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="19354-197">serveur Spark Thrift un Spark sur HDInsight cluster, utilisez port tooconnect toohello `10002` au lieu de `10001`.</span><span class="sxs-lookup"><span data-stu-id="19354-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="19354-198">Par exemple, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="19354-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19354-199">serveur de Spark Thrift Hello est pas directement accessibles sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="19354-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="19354-200">Vous pouvez uniquement vous connecter tooit à partir d’une session SSH ou à l’intérieur de hello même réseau virtuel Azure comme hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19354-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="19354-201"><a id="summary"></a><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19354-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="19354-202">Pour des informations générales sur Hive dans HDInsight, consultez hello suivant du document :</span><span class="sxs-lookup"><span data-stu-id="19354-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="19354-203">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="19354-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="19354-204">Pour plus d’informations sur d’autres méthodes que vous pouvez travailler avec Hadoop dans HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="19354-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="19354-205">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="19354-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="19354-206">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="19354-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="19354-207">Si vous utilisez Tez avec Hive, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="19354-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="19354-208">Utilisez hello Tez UI sur HDInsight de basés sur Windows</span><span class="sxs-lookup"><span data-stu-id="19354-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="19354-209">Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="19354-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
