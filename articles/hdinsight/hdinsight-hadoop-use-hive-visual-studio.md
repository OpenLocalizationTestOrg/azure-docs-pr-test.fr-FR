---
title: aaaHive avec les outils Data Lake (Hadoop) pour Visual Studio - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse hello Data Lake tools pour Visual Studio les toorun Apache Hive requêtes avec Apache Hadoop sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7d4b1-103">Exécuter des requêtes Hive à l’aide des outils de Data Lake hello pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d4b1-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7d4b1-104">Découvrez comment toouse hello Data Lake tools pour Visual Studio les tooquery Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="7d4b1-105">Hello Data Lake outils permettent de tooeasily créer, soumettre et surveiller tooHadoop des requêtes Hive sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="7d4b1-106"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7d4b1-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7d4b1-107">Un cluster Azure HDInsight sous Linux (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="7d4b1-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7d4b1-108">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7d4b1-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7d4b1-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7d4b1-110">(L’une des versions suivantes de hello) de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="7d4b1-111">Visual Studio 2013 Community/Professional/Premium/Ultimate avec mise à jour 4</span><span class="sxs-lookup"><span data-stu-id="7d4b1-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="7d4b1-112">Visual Studio 2015 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="7d4b1-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="7d4b1-113">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="7d4b1-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="7d4b1-114">Outils HDInsight pour Visual Studio ou Outils Azure Data Lake pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="7d4b1-115">Consultez [prise en main des outils de Visual Studio Hadoop pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) pour plus d’informations sur l’installation et configuration des outils de hello.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="7d4b1-116"><a id="run"></a>Exécuter des requêtes Hive à l’aide de hello Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d4b1-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="7d4b1-117">Ouvrez **Visual Studio** et sélectionnez **Nouveau** > **Projet** > **Azure Data Lake** > **HIVE** > **Application Hive**.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="7d4b1-118">Fournissez un nom pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="7d4b1-119">Ouvrez hello **Script.hql** fichier est créé avec ce projet et le coller dans hello suivant les instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="7d4b1-120">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7d4b1-121">`DROP TABLE`: Si la table de hello existe, cette instruction supprime.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="7d4b1-122">`CREATE EXTERNAL TABLE` : crée une table externe dans Hive.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="7d4b1-123">Les tables externes ne stockent la définition de table hello Hive (hello données restent dans l’emplacement d’origine de hello).</span><span class="sxs-lookup"><span data-stu-id="7d4b1-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="7d4b1-124">Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="7d4b1-125">Par exemple, un travail MapReduce ou service Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="7d4b1-126">Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="7d4b1-127">`ROW FORMAT`: Indique la ruche de mise en forme les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="7d4b1-128">Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="7d4b1-129">`STORED AS TEXTFILE LOCATION`: Indique ruche où hello les données sont stockées (répertoire de données d’exemple hello) et qu’il est stocké sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="7d4b1-130">`SELECT`: Permet de sélectionner un nombre de toutes les lignes où colonne `t4` contient la valeur de hello `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="7d4b1-131">Cette instruction renvoie la valeur `3`, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="7d4b1-132">`INPUT__FILE__NAME LIKE '%.log'` : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="7d4b1-133">Cette clause limite hello recherche toohello exemple.log fichier qui contient les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="7d4b1-134">Dans la barre d’outils de hello, sélectionnez hello **HDInsight Cluster** que vous souhaitez toouse pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="7d4b1-135">Sélectionnez **Submit** toorun les instructions de hello en tant qu’un travail Hive.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Barre d’envoi](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="7d4b1-137">Hello **récapitulatif de la ruche** apparaît et affiche des informations sur hello travail en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="7d4b1-138">Hello d’utilisation **Actualiser** lien toorefresh hello informations sur les travaux, jusqu'à ce que hello **état du travail** change également**terminé**.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![résumé de tâche affichant un travail terminé](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="7d4b1-140">Hello d’utilisation **sortie des tâches** lien de sortie de hello tooview de ce travail.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="7d4b1-141">Il affiche `[ERROR] 3`, qui est la valeur hello retourné par cette requête.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="7d4b1-142">Vous pouvez également exécuter des requêtes Hive sans créer de projet.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="7d4b1-143">À l’aide de l’**Explorateur de serveurs**, développez **Azure** > **HDInsight**, cliquez avec le bouton droit sur votre serveur HDInsight, puis sélectionnez **Écrire une requête Hive**.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="7d4b1-144">Bonjour **temp.hql** document qui s’affiche, ajoutez hello suivant les instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="7d4b1-145">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7d4b1-146">`CREATE TABLE IF NOT EXISTS` : crée une table, si elle n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="7d4b1-147">Étant donné que hello `EXTERNAL` mot clé n’est pas utilisé, cette instruction crée une table interne.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="7d4b1-148">Tables internes sont stockées dans l’entrepôt de données Hive hello et sont gérés par la ruche.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7d4b1-149">Contrairement aux `EXTERNAL` supprime les tables, suppression d’une table interne également hello les données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="7d4b1-150">`STORED AS ORC`: Stocke hello données ligne optimisé (ORC) sous forme de colonnes.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="7d4b1-151">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="7d4b1-152">`INSERT OVERWRITE ... SELECT`: Sélectionne des lignes à partir de hello `log4jLogs` table qui contiennent des `[ERROR]`, puis insère hello des données dans hello `errorLogs` table.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="7d4b1-153">Barre d’outils du hello **Submit** tâche hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="7d4b1-154">Hello d’utilisation **état du travail** toodetermine que hello est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="7d4b1-155">tooverify qui hello travail créé la table hello, utilisez **l’Explorateur de serveurs** et développez **Azure** > **HDInsight** > votre cluster HDInsight > **Bases de données de la ruche** > **par défaut**.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="7d4b1-156">Hello **journaux d’erreurs** table et hello **log4jLogs** table sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="7d4b1-157"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d4b1-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7d4b1-158">Comme vous pouvez le voir, hello HDInsight pour Visual Studio garantissent une toowork facilement avec les requêtes Hive dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7d4b1-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="7d4b1-159">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="7d4b1-160">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d4b1-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="7d4b1-161">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7d4b1-162">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d4b1-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="7d4b1-163">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="7d4b1-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7d4b1-164">Pour plus d’informations sur les outils HDInsight hello pour Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="7d4b1-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="7d4b1-165">Prise en main des outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d4b1-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
