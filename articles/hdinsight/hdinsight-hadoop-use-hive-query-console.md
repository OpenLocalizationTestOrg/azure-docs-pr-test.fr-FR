---
title: "Utiliser Hadoop Hive sur la console de requêtes dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment utiliser la console de requêtes Web pour exécuter des requêtes Hive sur un cluster Hadoop HDInsight à partir de votre navigateur."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="bc64e-103">Exécution de requêtes Hive à l'aide de la console de requêtes</span><span class="sxs-lookup"><span data-stu-id="bc64e-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="bc64e-104">Dans cet article, vous découvrirez comment utiliser la console de requêtes HDInsight pour exécuter des requêtes Hive sur un cluster Hadoop HDInsight à partir de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="bc64e-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc64e-105">La console de requêtes HDInsight n’est disponible que sur les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="bc64e-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="bc64e-106">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="bc64e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bc64e-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bc64e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="bc64e-108">Pour HDInsight 3.4 ou version supérieure, consultez [Run Hive queries in Ambari Hive View (Exécution de requêtes Hive dans la vue Hive d’Ambari)](hdinsight-hadoop-use-hive-ambari-view.md) pour plus d’informations sur l’exécution de requêtes Hive à partir d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="bc64e-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="bc64e-109"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="bc64e-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="bc64e-110">Pour effectuer les étapes présentées dans cet article, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bc64e-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="bc64e-111">Un cluster Hadoop HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="bc64e-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="bc64e-112">Un navigateur Web moderne</span><span class="sxs-lookup"><span data-stu-id="bc64e-112">A modern web browser</span></span>

## <span data-ttu-id="bc64e-113"><a id="run"></a> Exécution de requêtes Hive à l'aide de la console de requêtes</span><span class="sxs-lookup"><span data-stu-id="bc64e-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="bc64e-114">Dans un navigateur web, accédez à l’adresse **https://CLUSTERNAME.azurehdinsight.net**, où **CLUSTERNAME** est le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc64e-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="bc64e-115">Lorsque vous y êtes invité, entrez le nom d'utilisateur et le mot de passe que vous avez entrés lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="bc64e-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="bc64e-116">À partir des liens situés en haut de la page, sélectionnez **Éditeur Hive**.</span><span class="sxs-lookup"><span data-stu-id="bc64e-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="bc64e-117">Cela affiche un formulaire qui peut être utilisé pour saisir les instructions HiveQL que vous souhaitez exécuter sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bc64e-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![l’éditeur Hive](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="bc64e-119">Remplacez le texte `Select * from hivesampletable` par les instructions HiveSQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="bc64e-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="bc64e-120">Ces instructions effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bc64e-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="bc64e-121">**DROP TABLE**: supprime la table et le fichier de données, si la table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="bc64e-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="bc64e-122">**CREATE EXTERNAL TABLE**: crée une table « externe » dans Hive.</span><span class="sxs-lookup"><span data-stu-id="bc64e-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="bc64e-123">Les tables externes stockent uniquement la définition de table dans Hive ; les données restent à leur emplacement d’origine.</span><span class="sxs-lookup"><span data-stu-id="bc64e-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="bc64e-124">Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe (comme un processus de téléchargement de données automatisé) ou par une autre opération MapReduce, mais souhaitez toujours que les requêtes Hive utilisent les données les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="bc64e-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="bc64e-125">La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.</span><span class="sxs-lookup"><span data-stu-id="bc64e-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="bc64e-126">**ROW FORMAT**: indique à Hive le mode de formatage des données.</span><span class="sxs-lookup"><span data-stu-id="bc64e-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="bc64e-127">Dans ce cas, les champs de chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="bc64e-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="bc64e-128">**STORED AS TEXTFILE LOCATION**: indique à Hive l'emplacement des données (le répertoire exemple/données) et précise qu'elles sont stockées sous la forme de texte.</span><span class="sxs-lookup"><span data-stu-id="bc64e-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="bc64e-129">**SELECT** : sélectionne toutes les lignes dont la colonne **t4** contient la valeur **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="bc64e-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="bc64e-130">Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="bc64e-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="bc64e-131">**INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="bc64e-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="bc64e-132">Cela limite la recherche au fichier sample.log qui contient les données et l'empêche de renvoyer des données provenant d'autres fichiers d'exemple qui ne correspondent pas au schéma que nous avons défini.</span><span class="sxs-lookup"><span data-stu-id="bc64e-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="bc64e-133">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="bc64e-133">Click **Submit**.</span></span> <span data-ttu-id="bc64e-134">La **session de la tâche** située au bas de la page devrait afficher les détails de la tâche.</span><span class="sxs-lookup"><span data-stu-id="bc64e-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="bc64e-135">Une fois le champ **État** défini sur **Terminé**, sélectionnez **Afficher les détails** de la tâche.</span><span class="sxs-lookup"><span data-stu-id="bc64e-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="bc64e-136">Dans la page relative aux détails, la **sortie de la tâche** contient `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="bc64e-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="bc64e-137">Vous pouvez utiliser le bouton **Télécharger** , situé en dessous de ce champ, pour télécharger un fichier contenant la sortie de la tâche.</span><span class="sxs-lookup"><span data-stu-id="bc64e-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="bc64e-138"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="bc64e-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="bc64e-139">Comme vous pouvez le constater, la console de requêtes permet d'exécuter facilement des requêtes Hive sur un cluster HDInsight, de surveiller l'état de la tâche et de récupérer le résultat.</span><span class="sxs-lookup"><span data-stu-id="bc64e-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="bc64e-140">Pour en savoir plus sur l’utilisation de la console de requêtes Hive pour l’exécution de tâches Hive, sélectionnez **Prise en main** en haut de la console de requêtes, puis utilisez les exemples fournis.</span><span class="sxs-lookup"><span data-stu-id="bc64e-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="bc64e-141">Chaque exemple aborde le processus d'analyse de données à l'aide de Hive, y compris les explications des instructions HiveQL utilisées dans l'exemple.</span><span class="sxs-lookup"><span data-stu-id="bc64e-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="bc64e-142"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc64e-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="bc64e-143">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="bc64e-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="bc64e-144">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc64e-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="bc64e-145">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="bc64e-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="bc64e-146">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc64e-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="bc64e-147">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc64e-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="bc64e-148">Si vous utilisez Tez avec Hive, consultez les documents suivants pour les informations de débogage :</span><span class="sxs-lookup"><span data-stu-id="bc64e-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="bc64e-149">Utiliser l'interface utilisateur Tez sur HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="bc64e-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="bc64e-150">Utilisez la vue Tez Ambari sur HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="bc64e-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
