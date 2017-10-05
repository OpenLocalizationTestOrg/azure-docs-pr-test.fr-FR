---
title: "Utiliser Hadoop Hive et le Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment vous connecter à un cluster Hadoop à l'aide du Bureau à distance, et exécuter ensuite des requêtes Hive à l'aide de l'interface de ligne de commande (CLI) Hive."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="c4f5e-103">Utilisation de Hive avec Hadoop sur HDInsight via le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="c4f5e-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="c4f5e-104">Dans cet article, vous découvrirez comment vous connecter à un cluster HDInsight à l'aide du Bureau à distance, et exécuter ensuite des requêtes Hive à l'aide de l'interface de ligne de commande (CLI) Hive.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4f5e-105">Le Bureau à distance n’est disponible que sur les clusters HDInsight qui utilisent Windows comme système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="c4f5e-106">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c4f5e-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c4f5e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="c4f5e-108">Pour HDInsight 3.4 ou les versions supérieures, consultez l’article [Utilisation de Hive avec Hadoop dans HDInsight via Beeline](hdinsight-hadoop-use-hive-beeline.md) pour plus d’informations sur l’exécution de requêtes Hive directement sur le cluster à partir d’une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="c4f5e-109"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="c4f5e-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="c4f5e-110">Pour effectuer les étapes présentées dans cet article, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="c4f5e-111">un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="c4f5e-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="c4f5e-112">Un ordinateur client avec Windows 10, Windows 8 ou Windows 7</span><span class="sxs-lookup"><span data-stu-id="c4f5e-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="c4f5e-113"><a id="connect"></a>Connexion avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="c4f5e-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="c4f5e-114">Activez le Bureau à distance pour le cluster HDInsight, puis connectez-vous à lui en suivant les instructions fournies dans [Connexion à des clusters HDInsight avec RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="c4f5e-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="c4f5e-115"><a id="hive"></a>Utilisation de la commande Hive</span><span class="sxs-lookup"><span data-stu-id="c4f5e-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="c4f5e-116">Une fois connecté au bureau pour le cluster HDInsight, effectuez les étapes suivantes pour utiliser Hive.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="c4f5e-117">À partir du bureau HDInsight, démarrez la **ligne de commande Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="c4f5e-118">Exécutez la commande suivante pour démarrer l'interface de ligne de commande (CLI) Hive :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="c4f5e-119">Une fois l'interface de ligne de commande lancée, vous verrez apparaître l'invite CLI : `hive>`.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="c4f5e-120">En utilisant l'interface de ligne de commande, saisissez les instructions suivantes pour créer une table nommée **log4jLogs** à l'aide d'exemples de données :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="c4f5e-121">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="c4f5e-122">**DROP TABLE**: supprime la table et le fichier de données, si la table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="c4f5e-123">**CREATE EXTERNAL TABLE**: crée une table externe dans Hive.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="c4f5e-124">Les tables externes stockent uniquement la définition de table dans Hive (les données restent à leur emplacement d’origine).</span><span class="sxs-lookup"><span data-stu-id="c4f5e-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="c4f5e-125">Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe (comme un processus de téléchargement de données automatisé) ou par une autre opération MapReduce, mais souhaitez toujours que les requêtes Hive utilisent les données les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="c4f5e-126">La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="c4f5e-127">**ROW FORMAT**: indique à Hive le mode de formatage des données.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="c4f5e-128">Dans ce cas, les champs de chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="c4f5e-129">**STORED AS TEXTFILE LOCATION**: indique à Hive l'emplacement des données (le répertoire exemple/données) et précise qu'elles sont stockées sous la forme de texte.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="c4f5e-130">**SELECT** : sélectionne toutes les lignes dont la colonne **t4** contient la valeur **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="c4f5e-131">Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="c4f5e-132">**INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="c4f5e-133">Cela limite la recherche au fichier sample.log qui contient les données et l'empêche de renvoyer des données provenant d'autres fichiers d'exemple qui ne correspondent pas au schéma que nous avons défini.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="c4f5e-134">Utilisez les instructions suivantes pour créer une table « interne » nommée **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="c4f5e-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="c4f5e-135">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="c4f5e-136">**CREATE TABLE IF NOT EXISTS**: crée une table, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="c4f5e-137">Le mot-clé **EXTERNAL** n’étant pas utilisé, il s’agit d’une table interne, stockée dans l’entrepôt de données Hive et gérée intégralement par Hive.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c4f5e-138">Contrairement aux tables **EXTERNES** , la suppression d’une table interne entraîne également la suppression des données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="c4f5e-139">**STORED AS ORC**: stocke les données au format ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="c4f5e-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="c4f5e-140">Il s'agit d'un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="c4f5e-141">**INSERT OVERWRITE ... SELECT** : sélectionne des lignes de la table **log4jLogs** qui contiennent **[ERROR]**, puis insère les données dans la table **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="c4f5e-142">Pour vérifier que seules les lignes contenant **[ERROR]** dans la colonne t4 ont été stockées dans la table **errorLogs**, utilisez l’instruction suivante afin de renvoyer toutes les lignes à partir de **errorLogs** :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="c4f5e-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="c4f5e-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="c4f5e-144">Trois lignes de données doivent normalement être renvoyées. Elles contiennent toutes **[ERROR]** dans la colonne t4.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="c4f5e-145"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="c4f5e-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="c4f5e-146">Comme vous pouvez le constater, la commande Hive permet d'exécuter facilement, et de façon interactive, des requêtes Hive sur un cluster HDInsight, de surveiller l'état de la tâche et de récupérer le résultat.</span><span class="sxs-lookup"><span data-stu-id="c4f5e-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="c4f5e-147"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4f5e-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="c4f5e-148">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="c4f5e-149">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4f5e-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="c4f5e-150">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c4f5e-151">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4f5e-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c4f5e-152">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4f5e-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c4f5e-153">Si vous utilisez Tez avec Hive, consultez les documents suivants pour les informations de débogage :</span><span class="sxs-lookup"><span data-stu-id="c4f5e-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="c4f5e-154">Utiliser l'interface utilisateur Tez sur HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="c4f5e-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="c4f5e-155">Utilisez la vue Tez Ambari sur HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="c4f5e-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
