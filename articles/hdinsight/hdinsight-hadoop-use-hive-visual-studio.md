---
title: "Hive avec les outils Data Lake (Hadoop) pour Visual Studio - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment utiliser les outils Data Lake pour Visual Studio pour exécuter des requêtes Apache Hive avec Apache Hadoop sur Azure HDInsight."
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
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="42921-103">Exécution de requêtes Hive à l’aide des outils Data Lake pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42921-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="42921-104">Découvrez comment utiliser les outils Data Lake pour Visual Studio pour interroger Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="42921-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="42921-105">Les outils Data Lake vous permettent de facilement créer, soumettre et surveiller les requêtes Hive à Hadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="42921-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="42921-106"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="42921-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="42921-107">Un cluster Azure HDInsight sous Linux (Hadoop sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="42921-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="42921-108">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="42921-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42921-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="42921-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="42921-110">Visual Studio (l'une des versions suivantes) :</span><span class="sxs-lookup"><span data-stu-id="42921-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="42921-111">Visual Studio 2013 Community/Professional/Premium/Ultimate avec mise à jour 4</span><span class="sxs-lookup"><span data-stu-id="42921-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="42921-112">Visual Studio 2015 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="42921-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="42921-113">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="42921-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="42921-114">Outils HDInsight pour Visual Studio ou Outils Azure Data Lake pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42921-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="42921-115">Consultez la page [Prise en main des outils Hadoop de Visual Studio pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) pour connaître les étapes d’installation et de configuration des outils.</span><span class="sxs-lookup"><span data-stu-id="42921-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="42921-116"><a id="run"></a> Exécution de requêtes Hive avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42921-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="42921-117">Ouvrez **Visual Studio** et sélectionnez **Nouveau** > **Projet** > **Azure Data Lake** > **HIVE** > **Application Hive**.</span><span class="sxs-lookup"><span data-stu-id="42921-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="42921-118">Fournissez un nom pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="42921-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="42921-119">Ouvrez le fichier **Script.hql** créé avec ce projet et collez les instructions HiveQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="42921-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="42921-120">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="42921-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="42921-121">`DROP TABLE`: si la table existe, cette instruction la supprime.</span><span class="sxs-lookup"><span data-stu-id="42921-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="42921-122">`CREATE EXTERNAL TABLE` : crée une table externe dans Hive.</span><span class="sxs-lookup"><span data-stu-id="42921-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="42921-123">Les tables externes stockent uniquement la définition de table dans Hive (les données restent à leur emplacement d’origine).</span><span class="sxs-lookup"><span data-stu-id="42921-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="42921-124">Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe,</span><span class="sxs-lookup"><span data-stu-id="42921-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="42921-125">Par exemple, un travail MapReduce ou service Azure.</span><span class="sxs-lookup"><span data-stu-id="42921-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="42921-126">La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.</span><span class="sxs-lookup"><span data-stu-id="42921-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="42921-127">`ROW FORMAT` : indique à Hive le mode de formatage des données.</span><span class="sxs-lookup"><span data-stu-id="42921-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="42921-128">Dans ce cas, les champs de chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="42921-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="42921-129">`STORED AS TEXTFILE LOCATION` : indique à Hive où sont stockées les données (répertoire example/data) et qu'elles sont stockées sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="42921-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="42921-130">`SELECT` : sélectionne toutes les lignes dont la colonne `t4` contient la valeur `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="42921-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="42921-131">Cette instruction renvoie la valeur `3`, car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="42921-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="42921-132">`INPUT__FILE__NAME LIKE '%.log'` : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="42921-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="42921-133">Cette clause limite la recherche au fichier sample.log qui contient les données.</span><span class="sxs-lookup"><span data-stu-id="42921-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="42921-134">Dans la barre d’outils, sélectionnez le **cluster HDInsight** que vous souhaitez utiliser pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="42921-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="42921-135">Sélectionnez **Envoyer** pour exécuter les instructions en tant que tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="42921-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Barre d’envoi](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="42921-137">Le **résumé de tâche Hive** apparaît et affiche des informations sur la tâche en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="42921-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="42921-138">Utilisez le lien **Actualiser** pour actualiser les informations sur la tâche, jusqu’à ce que l’**état de la tâche** passe à **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="42921-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![résumé de tâche affichant un travail terminé](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="42921-140">Utilisez le lien **Sortie de la tâche** pour afficher la sortie de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="42921-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="42921-141">Il affiche `[ERROR] 3`, soit la valeur retournée par cette requête.</span><span class="sxs-lookup"><span data-stu-id="42921-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="42921-142">Vous pouvez également exécuter des requêtes Hive sans créer de projet.</span><span class="sxs-lookup"><span data-stu-id="42921-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="42921-143">À l’aide de l’**Explorateur de serveurs**, développez **Azure** > **HDInsight**, cliquez avec le bouton droit sur votre serveur HDInsight, puis sélectionnez **Écrire une requête Hive**.</span><span class="sxs-lookup"><span data-stu-id="42921-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="42921-144">Dans le document **temp.hql** qui s’affiche, ajoutez les instructions HiveQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="42921-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="42921-145">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="42921-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="42921-146">`CREATE TABLE IF NOT EXISTS` : crée une table, si elle n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="42921-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="42921-147">Étant donné que le mot-clé `EXTERNAL` n’est pas utilisé, cette instruction crée une table interne.</span><span class="sxs-lookup"><span data-stu-id="42921-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="42921-148">Les tables internes sont stockées dans l’entrepôt de données Hive et gérées par Hive.</span><span class="sxs-lookup"><span data-stu-id="42921-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="42921-149">Contrairement aux tables `EXTERNAL`, la suppression d’une table interne entraîne également la suppression des données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="42921-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="42921-150">`STORED AS ORC` : stocke les données dans un format ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="42921-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="42921-151">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="42921-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="42921-152">`INSERT OVERWRITE ... SELECT`: sélectionne des lignes de la table `log4jLogs` qui contiennent `[ERROR]`, puis insère les données dans la table `errorLogs`.</span><span class="sxs-lookup"><span data-stu-id="42921-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="42921-153">Dans la barre d’outils, sélectionnez la liste déroulante pour **Envoyer** , afin d’exécuter la tâche.</span><span class="sxs-lookup"><span data-stu-id="42921-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="42921-154">Utilisez l’ **état de la tâche** afin de déterminer si la tâche est terminée.</span><span class="sxs-lookup"><span data-stu-id="42921-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="42921-155">Pour vérifier que le travail a créé une table, utilisez **Explorateur de serveurs** et développez **Azure** > **HDInsight** > votre cluster HDInsight > **Bases de données Hive** > **par défaut**.</span><span class="sxs-lookup"><span data-stu-id="42921-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="42921-156">La table **errorLogs** et la table **log4jLogs** sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="42921-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="42921-157"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42921-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="42921-158">Comme vous pouvez le voir, les outils HDInsight pour Visual Studio fournissent un moyen simple de travailler avec des requêtes Hive sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="42921-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="42921-159">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="42921-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="42921-160">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="42921-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="42921-161">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="42921-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="42921-162">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="42921-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="42921-163">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="42921-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="42921-164">Pour plus d’informations sur les outils de HDInsight pour Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="42921-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="42921-165">Prise en main des outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42921-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
