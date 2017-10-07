---
title: "aaaUse Hadoop Hive et Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment tooconnect tooHadoop cluster HDInsight à l’aide du Bureau à distance, puis exécuter des requêtes Hive à l’aide de hello Hive une Interface de ligne."
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
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="aee69-103">Utilisation de Hive avec Hadoop sur HDInsight via le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="aee69-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="aee69-104">Dans cet article, vous allez apprendre comment tooconnect tooan HDInsight cluster à l’aide du Bureau à distance, puis exécutez la ruche de requêtes à l’aide de hello Hive d’Interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="aee69-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aee69-105">Bureau à distance n’est disponible sur les clusters HDInsight utilisent Windows comme système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="aee69-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="aee69-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="aee69-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aee69-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aee69-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="aee69-108">Pour HDInsight 3.4 ou supérieure, consultez [utilisez Hive avec HDInsight et Beeline](hdinsight-hadoop-use-hive-beeline.md) pour plus d’informations sur l’exécution des requêtes Hive directement sur le cluster de hello à partir d’une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="aee69-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="aee69-109"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="aee69-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="aee69-110">toocomplete hello étapes décrites dans cet article, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="aee69-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="aee69-111">un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="aee69-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="aee69-112">Un ordinateur client avec Windows 10, Windows 8 ou Windows 7</span><span class="sxs-lookup"><span data-stu-id="aee69-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="aee69-113"><a id="connect"></a>Connexion avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="aee69-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="aee69-114">Activer le Bureau à distance pour le cluster HDInsight de hello, puis connecter tooit en suivant les instructions de hello sur [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="aee69-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="aee69-115"><a id="hive"></a>Utilisez la commande de ruche hello</span><span class="sxs-lookup"><span data-stu-id="aee69-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="aee69-116">Lorsque vous avez connecté bureau toohello pour le cluster HDInsight de hello, utilisez hello suivant toowork étapes avec Hive :</span><span class="sxs-lookup"><span data-stu-id="aee69-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="aee69-117">À partir du bureau de HDInsight hello, démarrer hello **ligne de commande Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="aee69-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="aee69-118">Entrez hello suivant commande toostart hello la ruche de CLI :</span><span class="sxs-lookup"><span data-stu-id="aee69-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="aee69-119">Lorsque hello CLI a démarré, vous verrez invite CLI de la ruche de hello : `hive>`.</span><span class="sxs-lookup"><span data-stu-id="aee69-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="aee69-120">À l’aide de hello CLI, entrez hello suivant les instructions toocreate une nouvelle table nommée **log4jLogs** à l’aide des exemples de données :</span><span class="sxs-lookup"><span data-stu-id="aee69-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="aee69-121">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="aee69-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="aee69-122">**DROP TABLE**: supprime la table de hello et le fichier de données hello si hello table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="aee69-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="aee69-123">**CREATE EXTERNAL TABLE**: crée une table « externe » dans Hive.</span><span class="sxs-lookup"><span data-stu-id="aee69-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="aee69-124">Tables externes stockent uniquement la définition de table hello dans la ruche (hello données restent dans l’emplacement d’origine de hello).</span><span class="sxs-lookup"><span data-stu-id="aee69-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="aee69-125">Tables externes doivent être utilisés lorsque vous attendez hello sous-jacent toobe de données mis à jour par une source externe (par exemple, un processus de téléchargement automatique des données) ou par une autre opération MapReduce, mais souhaitez toujours que ruche interroge les données les plus récentes toouse hello.</span><span class="sxs-lookup"><span data-stu-id="aee69-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="aee69-126">Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.</span><span class="sxs-lookup"><span data-stu-id="aee69-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="aee69-127">**FORMAT de ligne**: indique la mise en forme les données de salutation ruche.</span><span class="sxs-lookup"><span data-stu-id="aee69-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="aee69-128">Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="aee69-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="aee69-129">**EMPLACEMENT du fichier texte comme stockées**: indique la ruche où les données de salutation sont stocké (répertoire de données d’exemple hello) et qu’il est stockée sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="aee69-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="aee69-130">**Sélectionnez**: sélectionne un nombre de toutes les lignes où colonne **t4** contient la valeur de hello **[erreur]**.</span><span class="sxs-lookup"><span data-stu-id="aee69-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="aee69-131">Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="aee69-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="aee69-132">**INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="aee69-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="aee69-133">Cela limite hello recherche toohello exemple.log fichier qui contient les données de salutation et empêche de renvoi de données à partir de l’autre exemple de fichiers de données qui ne correspondent pas aux schéma hello que nous avons défini.</span><span class="sxs-lookup"><span data-stu-id="aee69-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="aee69-134">Hello utilisation suivant les instructions toocreate une nouvelle table « interne » nommée **journaux d’erreurs de**:</span><span class="sxs-lookup"><span data-stu-id="aee69-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="aee69-135">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="aee69-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="aee69-136">**CREATE TABLE IF NOT EXISTS**: crée une table, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="aee69-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="aee69-137">Étant donné que hello **externe** mot clé n’est pas utilisé, il s’agit d’une table interne, qui est stockée dans l’entrepôt de données Hive hello et entièrement gérée par ruche.</span><span class="sxs-lookup"><span data-stu-id="aee69-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="aee69-138">Contrairement aux **externe** supprime les tables, suppression d’une table interne également hello les données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="aee69-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="aee69-139">**STOCKÉES des ORC AS**: stocke les données de hello ligne optimisé (ORC) sous forme de colonnes.</span><span class="sxs-lookup"><span data-stu-id="aee69-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="aee69-140">Il s'agit d'un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="aee69-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="aee69-141">**INSERT OVERWRITE ... Sélectionnez**: sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des **[erreur]**, puis insère hello des données dans hello **journaux d’erreurs de** table.</span><span class="sxs-lookup"><span data-stu-id="aee69-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="aee69-142">tooverify que seules les lignes qui contiennent **[erreur]** dans la colonne t4 étaient stockée toohello **journaux d’erreurs** table, utilisez hello suivant tooreturn instruction tous hello des lignes à partir de **journaux d’erreurs de**:</span><span class="sxs-lookup"><span data-stu-id="aee69-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="aee69-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="aee69-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="aee69-144">Trois lignes de données doivent normalement être renvoyées. Elles contiennent toutes **[ERROR]** dans la colonne t4.</span><span class="sxs-lookup"><span data-stu-id="aee69-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="aee69-145"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="aee69-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="aee69-146">Comme vous pouvez le voir, Bonjour Bonjour ruche commande fournit une toointeractively facilement exécuter des requêtes Hive sur un cluster HDInsight, hello d’analyse état du travail et d’extraire la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="aee69-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="aee69-147"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aee69-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="aee69-148">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="aee69-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="aee69-149">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="aee69-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="aee69-150">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="aee69-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="aee69-151">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="aee69-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="aee69-152">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="aee69-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="aee69-153">Si vous utilisez Tez avec Hive, consultez hello suivant des documents pour les informations de débogage :</span><span class="sxs-lookup"><span data-stu-id="aee69-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="aee69-154">Utilisez hello Tez UI sur HDInsight de basés sur Windows</span><span class="sxs-lookup"><span data-stu-id="aee69-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="aee69-155">Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="aee69-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
