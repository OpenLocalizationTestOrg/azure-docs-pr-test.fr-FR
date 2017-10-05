---
title: "Utiliser la vue Tez d’Ambari avec HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser la vue Tez d’Ambari pour déboguer les travaux Tez dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="58a45-103">Utiliser les vues Ambari pour déboguer les travaux Tez dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="58a45-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="58a45-104">L’interface utilisateur Web d’Ambari pour HDInsight contient une vue Tez qui peut servir à comprendre et à déboguer les tâches utilisant Tez.</span><span class="sxs-lookup"><span data-stu-id="58a45-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="58a45-105">La vue Tez vous permet de visualiser le travail sous forme de graphique d’éléments connectés, d’explorer chacun d’entre eux, ainsi que d’extraire des statistiques et des informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="58a45-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58a45-106">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="58a45-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="58a45-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="58a45-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="58a45-108">Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="58a45-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58a45-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="58a45-109">Prerequisites</span></span>

* <span data-ttu-id="58a45-110">Un cluster HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="58a45-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="58a45-111">Pour plus d’informations sur la création d’un cluster, consultez l’article [Prise en main de HDInsight sous Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58a45-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="58a45-112">Un navigateur web moderne qui prend en charge HTML5.</span><span class="sxs-lookup"><span data-stu-id="58a45-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="58a45-113">Présentation de Tez</span><span class="sxs-lookup"><span data-stu-id="58a45-113">Understanding Tez</span></span>

<span data-ttu-id="58a45-114">Tez est une infrastructure extensible pour le traitement des données dans Hadoop plus rapide que le traitement MapReduce traditionnel.</span><span class="sxs-lookup"><span data-stu-id="58a45-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="58a45-115">Pour les clusters HDInsight sous Linux, Tez est le moteur par défaut pour Hive.</span><span class="sxs-lookup"><span data-stu-id="58a45-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="58a45-116">Tez crée un graphe orienté acyclique qui décrit l’ordre des actions requises par les tâches.</span><span class="sxs-lookup"><span data-stu-id="58a45-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="58a45-117">Les actions individuelles sont appelées des vertex et exécutent une partie du travail global.</span><span class="sxs-lookup"><span data-stu-id="58a45-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="58a45-118">L’exécution réelle du travail décrit par un vertex est appelée une tâche, et peut être répartie sur plusieurs nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="58a45-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="58a45-119">Présentation de la vue Tez</span><span class="sxs-lookup"><span data-stu-id="58a45-119">Understanding the Tez view</span></span>

<span data-ttu-id="58a45-120">La vue Tez fournit des informations historiques et des informations sur les processus en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="58a45-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="58a45-121">Ces informations vous indiquent comment une tâche est répartie entre les clusters.</span><span class="sxs-lookup"><span data-stu-id="58a45-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="58a45-122">Elle affiche également les compteurs utilisés par les tâches et les vertex et les informations des erreurs liées à la tâche.</span><span class="sxs-lookup"><span data-stu-id="58a45-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="58a45-123">Elle peut fournir des informations utiles dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="58a45-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="58a45-124">Surveiller les processus à long terme, voir l'avancement des tâches de mappage et de réduction.</span><span class="sxs-lookup"><span data-stu-id="58a45-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="58a45-125">Analyser les données historiques des processus ayant réussi ou échoué, afin de savoir comment le traitement peut être amélioré ou pourquoi il a échoué.</span><span class="sxs-lookup"><span data-stu-id="58a45-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="58a45-126">Générer un DAG</span><span class="sxs-lookup"><span data-stu-id="58a45-126">Generate a DAG</span></span>

<span data-ttu-id="58a45-127">La vue Tez ne contient des données que si une tâche qui utilise le moteur Tez est en cours d’exécution ou a déjà été exécutée.</span><span class="sxs-lookup"><span data-stu-id="58a45-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="58a45-128">Les requêtes Hive simples peuvent être résolues sans utiliser Tez.</span><span class="sxs-lookup"><span data-stu-id="58a45-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="58a45-129">Les requêtes plus complexes qui effectuent des opérations de filtrage, de regroupement, de tri, de jointure, etc.</span><span class="sxs-lookup"><span data-stu-id="58a45-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="58a45-130">utilisent le moteur Tez.</span><span class="sxs-lookup"><span data-stu-id="58a45-130">use the Tez engine.</span></span>

<span data-ttu-id="58a45-131">Utilisez les étapes suivantes pour exécuter une requête Hive utilisant Tez :</span><span class="sxs-lookup"><span data-stu-id="58a45-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="58a45-132">Dans un navigateur web, accédez à l’adresse https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58a45-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="58a45-133">Dans le menu situé en haut de la page, sélectionnez l’icône **Vues** .</span><span class="sxs-lookup"><span data-stu-id="58a45-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="58a45-134">Cette icône représente une série de carrés.</span><span class="sxs-lookup"><span data-stu-id="58a45-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="58a45-135">Dans la liste déroulante qui s’affiche, sélectionnez **Vue Hive**.</span><span class="sxs-lookup"><span data-stu-id="58a45-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Sélectionner la vue Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="58a45-137">Une fois la vue Hive chargée, collez la requête suivante dans l’éditeur de requête, puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="58a45-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="58a45-138">Une fois le travail terminé, le résultat devrait s’afficher dans la section **Résultats du processus de requête** .</span><span class="sxs-lookup"><span data-stu-id="58a45-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="58a45-139">Les résultats doivent être similaires au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="58a45-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="58a45-140">Sélectionnez l’onglet **Journal**.</span><span class="sxs-lookup"><span data-stu-id="58a45-140">Select the **Log** tab.</span></span> <span data-ttu-id="58a45-141">Des informations similaires au texte suivant s’affichent :</span><span class="sxs-lookup"><span data-stu-id="58a45-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="58a45-142">Enregistrez la valeur **ID d’application** , car elle est utilisée dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="58a45-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="58a45-143">Utiliser la vue Tez</span><span class="sxs-lookup"><span data-stu-id="58a45-143">Use the Tez View</span></span>

1. <span data-ttu-id="58a45-144">Dans le menu situé en haut de la page, sélectionnez l’icône **Vues** .</span><span class="sxs-lookup"><span data-stu-id="58a45-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="58a45-145">Dans la liste déroulante qui s’affiche, sélectionnez **Vue Tez**.</span><span class="sxs-lookup"><span data-stu-id="58a45-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Sélectionner la vue Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="58a45-147">Une fois la vue Tez chargée, la liste des requêtes Hive en cours d’exécution ou exécutées sur le cluster s’affiche.</span><span class="sxs-lookup"><span data-stu-id="58a45-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Tous les DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="58a45-149">Si vous ne voyez qu’une seule entrée, il s’agit de la requête que vous avez exécutée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="58a45-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="58a45-150">Si vous avez plusieurs entrées, vous pouvez les rechercher en haut de la page à l’aide des champs.</span><span class="sxs-lookup"><span data-stu-id="58a45-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="58a45-151">Sélectionnez **l’ID de requête** pour une requête Hive.</span><span class="sxs-lookup"><span data-stu-id="58a45-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="58a45-152">De plus amples informations sur la requête s’affichent.</span><span class="sxs-lookup"><span data-stu-id="58a45-152">Information about the query is displayed.</span></span>

    ![Détails du DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="58a45-154">Les onglets de cette page vous permettent d’afficher les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="58a45-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="58a45-155">**Détails de la requête** : plus d’informations sur la requête Hive.</span><span class="sxs-lookup"><span data-stu-id="58a45-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="58a45-156">**Chronologie** : plus d’informations sur la durée de chaque étape du traitement.</span><span class="sxs-lookup"><span data-stu-id="58a45-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="58a45-157">**Configurations** : la configuration utilisée pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="58a45-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="58a45-158">À partir de __Détails de la requête__, vous pouvez utiliser les liens pour rechercher des informations sur __Application__ ou __DAG__ pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="58a45-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="58a45-159">Le lien __Application__ affiche des informations sur l’application YARN pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="58a45-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="58a45-160">À ce stade, vous pouvez accéder aux journaux des applications YARN.</span><span class="sxs-lookup"><span data-stu-id="58a45-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="58a45-161">Le lien __DAG__ affiche des informations sur le graphique acyclique dirigé pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="58a45-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="58a45-162">Cette vue permet d’afficher une représentation graphique du DAG.</span><span class="sxs-lookup"><span data-stu-id="58a45-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="58a45-163">Vous pouvez également rechercher des informations sur les vertex dans le DAG.</span><span class="sxs-lookup"><span data-stu-id="58a45-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58a45-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58a45-164">Next Steps</span></span>

<span data-ttu-id="58a45-165">Maintenant que vous avez appris à utiliser la vue Tez, obtenez plus d’informations sur l’ [Utilisation de Hive dans HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="58a45-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="58a45-166">Pour plus d’informations techniques sur Tez, consultez la [page Tez sur Hortonworks](http://hortonworks.com/hadoop/tez/)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="58a45-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="58a45-167">Pour plus d’informations sur l’utilisation d’Ambari avec HDInsight, consultez la page [Gérer des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="58a45-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
