---
title: aaaUse Ambari Tez vue HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse hello Ambari Tez afficher les travaux de Tez toodebug sur HDInsight."
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
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="10275-103">Utilisez les vues Ambari toodebug Tez travaux sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="10275-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="10275-104">Hello l’interface utilisateur Web de Ambari pour HDInsight contient une vue de Tez qui peut être utilisés des travaux de toounderstand et de débogage qui utilisent Tez.</span><span class="sxs-lookup"><span data-stu-id="10275-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="10275-105">vue de Tez Hello vous permet de travail de hello toovisualize comme un graphique des éléments connectés, explorez chaque élément et extraire des statistiques et informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="10275-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10275-106">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="10275-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="10275-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="10275-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="10275-108">Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="10275-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10275-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="10275-109">Prerequisites</span></span>

* <span data-ttu-id="10275-110">Un cluster HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="10275-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="10275-111">Pour plus d’informations sur la création d’un cluster, consultez l’article [Prise en main de HDInsight sous Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="10275-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="10275-112">Un navigateur web moderne qui prend en charge HTML5.</span><span class="sxs-lookup"><span data-stu-id="10275-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="10275-113">Présentation de Tez</span><span class="sxs-lookup"><span data-stu-id="10275-113">Understanding Tez</span></span>

<span data-ttu-id="10275-114">Tez est une infrastructure extensible pour le traitement des données dans Hadoop plus rapide que le traitement MapReduce traditionnel.</span><span class="sxs-lookup"><span data-stu-id="10275-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="10275-115">Pour les clusters HDInsight de basés sur Linux, il est moteur par défaut de hello pour la ruche.</span><span class="sxs-lookup"><span data-stu-id="10275-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="10275-116">Tez crée un dirigées acycliques graphique (DAG) qui décrit l’ordre de hello des actions requises par les travaux.</span><span class="sxs-lookup"><span data-stu-id="10275-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="10275-117">Différentes actions sont appelées des sommets et exécuter une partie de hello travail global.</span><span class="sxs-lookup"><span data-stu-id="10275-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="10275-118">l’exécution réelle de Hello de travail hello décrite par un sommet est appelée une tâche et peut être répartie sur plusieurs nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="10275-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="10275-119">Hello de présentation Tez vue</span><span class="sxs-lookup"><span data-stu-id="10275-119">Understanding hello Tez view</span></span>

<span data-ttu-id="10275-120">Hello Tez vue fournit des informations d’historique et des informations sur les processus qui sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="10275-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="10275-121">Ces informations vous indiquent comment une tâche est répartie entre les clusters.</span><span class="sxs-lookup"><span data-stu-id="10275-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="10275-122">Elle affiche également des compteurs utilisés par les tâches et les sommets, et des informations d’erreur liés toohello travail.</span><span class="sxs-lookup"><span data-stu-id="10275-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="10275-123">Il offre des informations utiles dans hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="10275-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="10275-124">Surveillance des processus longs, affichage hello la progression de la carte et réduire les tâches.</span><span class="sxs-lookup"><span data-stu-id="10275-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="10275-125">Analyse des données historiques pour les processus réussies ou échouées toolearn comment le traitement peut être amélioré ou en raison de l’échec.</span><span class="sxs-lookup"><span data-stu-id="10275-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="10275-126">Générer un DAG</span><span class="sxs-lookup"><span data-stu-id="10275-126">Generate a DAG</span></span>

<span data-ttu-id="10275-127">Hello Tez vue contient uniquement les données si une tâche qui utilise hello Tez moteur est en cours d’exécution ou a été exécuté précédemment.</span><span class="sxs-lookup"><span data-stu-id="10275-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="10275-128">Les requêtes Hive simples peuvent être résolues sans utiliser Tez.</span><span class="sxs-lookup"><span data-stu-id="10275-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="10275-129">Les requêtes plus complexes qui effectuent des opérations de filtrage, de regroupement, de tri, de jointure, etc.</span><span class="sxs-lookup"><span data-stu-id="10275-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="10275-130">Utilisez hello Tez moteur.</span><span class="sxs-lookup"><span data-stu-id="10275-130">use hello Tez engine.</span></span>

<span data-ttu-id="10275-131">Utilisez hello suivant les étapes toorun une requête Hive qui utilise Tez :</span><span class="sxs-lookup"><span data-stu-id="10275-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="10275-132">Dans un navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** hello désigne votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10275-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="10275-133">Dans le menu de hello en hello haut hello, sélectionnez hello **vues** icône.</span><span class="sxs-lookup"><span data-stu-id="10275-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="10275-134">Cette icône représente une série de carrés.</span><span class="sxs-lookup"><span data-stu-id="10275-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="10275-135">Dans la liste déroulante hello qui s’affiche, sélectionnez **Hive vue**.</span><span class="sxs-lookup"><span data-stu-id="10275-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Sélectionner la vue Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="10275-137">Lorsque hello ruche vue charge, coller hello ci-dessous dans l’éditeur de requête de hello de requête, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="10275-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="10275-138">Une fois le travail de hello est terminé, vous devez voir sortie hello affiché dans hello **résultats du processus de requête** section.</span><span class="sxs-lookup"><span data-stu-id="10275-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="10275-139">les résultats de Hello doivent être similaires toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="10275-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="10275-140">Sélectionnez hello **journal** onglet. Vous consultez toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="10275-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="10275-141">Enregistrer hello **id d’application** valeur, comme cette valeur est utilisée dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="10275-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="10275-142">Utilisez hello Tez vue</span><span class="sxs-lookup"><span data-stu-id="10275-142">Use hello Tez View</span></span>

1. <span data-ttu-id="10275-143">Dans le menu de hello en hello haut hello, sélectionnez hello **vues** icône.</span><span class="sxs-lookup"><span data-stu-id="10275-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="10275-144">Dans la liste déroulante hello qui s’affiche, sélectionnez **Tez vue**.</span><span class="sxs-lookup"><span data-stu-id="10275-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Sélectionner la vue Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="10275-146">Lors du chargement de hello Tez vue, vous voyez une liste de requêtes hive qui sont en cours d’exécution, ou qui ont été exécutés sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="10275-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Tous les DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="10275-148">Si vous avez une seule entrée, il est de requête hello que vous avez exécuté dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="10275-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="10275-149">Si vous avez plusieurs entrées, vous pouvez le rechercher à l’aide des champs de hello en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="10275-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="10275-150">Sélectionnez hello **ID de requête** pour une requête Hive.</span><span class="sxs-lookup"><span data-stu-id="10275-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="10275-151">Informations sur la requête de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="10275-151">Information about hello query is displayed.</span></span>

    ![Détails du DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="10275-153">onglets Hello sur cette page permettent de hello tooview informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="10275-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="10275-154">**Détails de la requête**: plus d’informations sur la requête de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="10275-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="10275-155">**Chronologie** : plus d’informations sur la durée de chaque étape du traitement.</span><span class="sxs-lookup"><span data-stu-id="10275-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="10275-156">**Configurations**: configuration hello utilisée pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="10275-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="10275-157">À partir de __détails de la requête__ vous pouvez utiliser hello liens toofind informations hello __Application__ ou hello __DAG__ pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="10275-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="10275-158">Hello __Application__ lien affiche des informations sur hello application fils pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="10275-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="10275-159">À ce stade, vous pouvez accéder à journaux d’application hello fils.</span><span class="sxs-lookup"><span data-stu-id="10275-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="10275-160">Hello __DAG__ lien affiche des informations sur le graphique acyclique dirigé de hello pour cette requête.</span><span class="sxs-lookup"><span data-stu-id="10275-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="10275-161">À ce stade, vous pouvez afficher une représentation graphique de hello DAG.</span><span class="sxs-lookup"><span data-stu-id="10275-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="10275-162">Vous trouverez également des informations sur les sommets hello dans hello DAG.</span><span class="sxs-lookup"><span data-stu-id="10275-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10275-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10275-163">Next Steps</span></span>

<span data-ttu-id="10275-164">Maintenant que vous avez appris comment toouse hello Tez afficher, en savoir plus sur [à l’aide de la ruche sur HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="10275-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="10275-165">Pour plus d’informations techniques sur Tez, consultez hello [page Tez sur Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="10275-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="10275-166">Pour plus d’informations sur l’utilisation de Ambari avec HDInsight, consultez [gérer les clusters HDInsight à l’aide de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="10275-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
