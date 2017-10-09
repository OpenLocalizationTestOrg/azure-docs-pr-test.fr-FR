---
title: "aaaUse Hadoop Hive sur hello Console de requête dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello basée sur le web Console de requête toorun requêtes Hive sur un HDInsight Hadoop de cluster à partir de votre navigateur."
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
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="b292c-103">Exécuter des requêtes Hive à l’aide de la Console de requête de hello</span><span class="sxs-lookup"><span data-stu-id="b292c-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="b292c-104">Dans cet article, vous allez apprendre comment les requêtes toouse hello Console de requête HDInsight toorun Hive sur un HDInsight Hadoop cluster depuis votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="b292c-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b292c-105">Hello Console de requête HDInsight est disponible uniquement sur les clusters HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="b292c-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="b292c-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="b292c-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b292c-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b292c-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="b292c-108">Pour HDInsight 3.4 ou version supérieure, consultez [Run Hive queries in Ambari Hive View (Exécution de requêtes Hive dans la vue Hive d’Ambari)](hdinsight-hadoop-use-hive-ambari-view.md) pour plus d’informations sur l’exécution de requêtes Hive à partir d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b292c-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="b292c-109"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="b292c-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="b292c-110">toocomplete hello étapes décrites dans cet article, vous devez suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="b292c-111">Un cluster Hadoop HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="b292c-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="b292c-112">Un navigateur Web moderne</span><span class="sxs-lookup"><span data-stu-id="b292c-112">A modern web browser</span></span>

## <span data-ttu-id="b292c-113"><a id="run"></a>Exécuter des requêtes Hive à l’aide de la Console de requête de hello</span><span class="sxs-lookup"><span data-stu-id="b292c-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="b292c-114">Ouvrez un navigateur web et accédez trop**https://CLUSTERNAME.azurehdinsight.net**, où **CLUSTERNAME** hello désigne votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b292c-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="b292c-115">Si vous y êtes invité, entrez le nom d’utilisateur hello et un mot de passe que vous avez utilisé lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="b292c-116">À partir des liens de hello en hello haut hello, sélectionnez **éditeur Hive**.</span><span class="sxs-lookup"><span data-stu-id="b292c-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="b292c-117">Cela affiche un formulaire qui peut être utilisé tooenter hello HiveQL instructions que vous souhaitez toorun dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![éditeur de ruche Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="b292c-119">Remplacez le texte hello `Select * from hivesampletable` avec hello suivant les instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="b292c-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="b292c-120">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="b292c-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="b292c-121">**DROP TABLE**: supprime la table de hello et le fichier de données hello si hello table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="b292c-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="b292c-122">**CREATE EXTERNAL TABLE**: crée une table « externe » dans Hive.</span><span class="sxs-lookup"><span data-stu-id="b292c-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="b292c-123">Tables externes stockent uniquement la définition de table hello dans la ruche ; les données de salutation reste dans l’emplacement d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b292c-124">Tables externes doivent être utilisés lorsque vous attendez hello sous-jacent toobe de données mis à jour par une source externe (par exemple, un processus de téléchargement automatique des données) ou par une autre opération MapReduce, mais souhaitez toujours que ruche interroge les données les plus récentes toouse hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="b292c-125">Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="b292c-126">**FORMAT de ligne**: indique la mise en forme les données de salutation ruche.</span><span class="sxs-lookup"><span data-stu-id="b292c-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="b292c-127">Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="b292c-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="b292c-128">**EMPLACEMENT du fichier texte comme stockées**: indique la ruche où les données de salutation sont stocké (répertoire de données d’exemple hello) et qu’il est stockée sous forme de texte</span><span class="sxs-lookup"><span data-stu-id="b292c-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="b292c-129">**Sélectionnez**: sélectionnez un nombre de toutes les lignes où colonne **t4** contiennent la valeur de hello **[erreur]**.</span><span class="sxs-lookup"><span data-stu-id="b292c-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="b292c-130">Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b292c-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="b292c-131">**INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log.</span><span class="sxs-lookup"><span data-stu-id="b292c-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="b292c-132">Cela limite hello recherche toohello exemple.log fichier qui contient les données de salutation et empêche de renvoi de données à partir de l’autre exemple de fichiers de données qui ne correspondent pas aux schéma hello que nous avons défini.</span><span class="sxs-lookup"><span data-stu-id="b292c-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="b292c-133">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="b292c-133">Click **Submit**.</span></span> <span data-ttu-id="b292c-134">Hello **Session de travail** à hello en bas de page de hello doit afficher les détails de tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="b292c-135">Hello lorsque **état** champ change trop**terminé**, sélectionnez **afficher les détails** pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="b292c-136">Sur la page de détails de hello, hello **sortie des tâches** contient `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="b292c-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="b292c-137">Vous pouvez utiliser hello **télécharger** bouton sous cette toodownload de champ d’un fichier qui contient la sortie de hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="b292c-138"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="b292c-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="b292c-139">Comme vous pouvez le voir, hello Console de requête fournit un moyen simple de toorun ruche les requêtes dans un cluster HDInsight, surveiller l’état de la tâche hello et récupérer la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="b292c-140">toolearn savoir plus sur l’aide de tâches de Console de requête Hive toorun Hive, sélectionnez **mise en route** haut hello de hello Console de requête, puis utiliser les exemples hello fournis.</span><span class="sxs-lookup"><span data-stu-id="b292c-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="b292c-141">Chaque exemple de guide de processus de hello d’à l’aide de la ruche tooanalyze données, y compris des explications sur les instructions HiveQL hello utilisées dans l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="b292c-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="b292c-142"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b292c-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="b292c-143">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="b292c-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="b292c-144">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b292c-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="b292c-145">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="b292c-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b292c-146">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b292c-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b292c-147">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b292c-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="b292c-148">Si vous utilisez Tez avec Hive, consultez hello suivant des documents pour les informations de débogage :</span><span class="sxs-lookup"><span data-stu-id="b292c-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="b292c-149">Utilisez hello Tez UI sur HDInsight de basés sur Windows</span><span class="sxs-lookup"><span data-stu-id="b292c-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="b292c-150">Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="b292c-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
