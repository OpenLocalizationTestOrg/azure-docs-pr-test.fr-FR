---
title: "Utiliser l'interface utilisateur Tez avec HDInsight basé sur Windows - Azure | Microsoft Docs"
description: "Apprenez à utiliser l'interface utilisateur Tez pour déboguer les travaux Tez dans HDInsight sous Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="35f5e-103">Utiliser l’interface utilisateur Tez pour déboguer les travaux Tez dans HDInsight sous Windows</span><span class="sxs-lookup"><span data-stu-id="35f5e-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="35f5e-104">L’interface utilisateur Tez est une page web qui peut servir à comprendre et à déboguer les travaux utilisant Tez comme moteur d’exécution pour les clusters HDInsight basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="35f5e-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="35f5e-105">L’interface utilisateur Tez vous permet de visualiser le travail sous forme de graphique d’éléments connectés, d’explorer chacun d’entre eux, ainsi que d’extraire des statistiques et des informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="35f5e-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35f5e-106">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Windows.</span><span class="sxs-lookup"><span data-stu-id="35f5e-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="35f5e-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="35f5e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="35f5e-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="35f5e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35f5e-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="35f5e-109">Prerequisites</span></span>
* <span data-ttu-id="35f5e-110">Un cluster HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="35f5e-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="35f5e-111">Pour plus d’informations sur la création d’un cluster, consultez [Prise en main de HDInsight sur Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="35f5e-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="35f5e-112">L’interface utilisateur Tez est disponible uniquement pour les clusters HDInsight sur Windows créés après le 8 février 2016.</span><span class="sxs-lookup"><span data-stu-id="35f5e-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="35f5e-113">Un client Bureau à distance basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="35f5e-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="35f5e-114">Présentation de Tez</span><span class="sxs-lookup"><span data-stu-id="35f5e-114">Understanding Tez</span></span>
<span data-ttu-id="35f5e-115">Tez est une infrastructure extensible pour le traitement des données dans Hadoop plus rapide que le traitement MapReduce traditionnel.</span><span class="sxs-lookup"><span data-stu-id="35f5e-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="35f5e-116">Pour les clusters HDInsight basés sur Windows, il s’agit d’un moteur facultatif que vous pouvez activer pour Hive dans le cadre de votre requête Hive à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="35f5e-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="35f5e-117">Lorsque Tez reçoit un travail à effectuer, il crée un graphe orienté acyclique (Directed Acyclic Graph - DAG) qui décrit l’ordre d’exécution des actions requises.</span><span class="sxs-lookup"><span data-stu-id="35f5e-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="35f5e-118">Les actions individuelles sont appelées des vertex et exécutent une partie du travail global.</span><span class="sxs-lookup"><span data-stu-id="35f5e-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="35f5e-119">L’exécution réelle du travail décrit par un vertex est appelée une tâche, et peut être répartie sur plusieurs nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="35f5e-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="35f5e-120">Présentation de l’interface utilisateur Tez</span><span class="sxs-lookup"><span data-stu-id="35f5e-120">Understanding the Tez UI</span></span>
<span data-ttu-id="35f5e-121">L’interface utilisateur Tez est une page web qui fournit des informations sur les processus en cours d’exécution, ou qui ont été exécutés à l’aide de Tez.</span><span class="sxs-lookup"><span data-stu-id="35f5e-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="35f5e-122">Elle vous permet d'afficher le DAG généré par Tez, de connaître la répartition entre les clusters, et d'accéder aux compteurs tels que la mémoire utilisée par les tâches et les vertex, ainsi qu'aux informations d'erreur.</span><span class="sxs-lookup"><span data-stu-id="35f5e-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="35f5e-123">Elle peut fournir des informations utiles dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="35f5e-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="35f5e-124">Surveiller les processus à long terme, voir l'avancement des tâches de mappage et de réduction.</span><span class="sxs-lookup"><span data-stu-id="35f5e-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="35f5e-125">Analyser les données historiques des processus ayant réussi ou échoué, afin de savoir comment le traitement peut être amélioré ou pourquoi il a échoué.</span><span class="sxs-lookup"><span data-stu-id="35f5e-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="35f5e-126">Générer un DAG</span><span class="sxs-lookup"><span data-stu-id="35f5e-126">Generate a DAG</span></span>
<span data-ttu-id="35f5e-127">L'interface utilisateur Tez contient des données uniquement si une tâche qui utilise le moteur Tez est en cours d'exécution ou a déjà été exécutée.</span><span class="sxs-lookup"><span data-stu-id="35f5e-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="35f5e-128">Les requêtes Hive simples peuvent généralement être résolues sans utiliser Tez. Toutefois, Tez est généralement nécessaire pour les requêtes plus complexes destinées à filtrer, regrouper, classer, joindre, etc.</span><span class="sxs-lookup"><span data-stu-id="35f5e-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="35f5e-129">Utilisez les étapes suivantes pour exécuter une requête Hive à l'aide de Tez.</span><span class="sxs-lookup"><span data-stu-id="35f5e-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="35f5e-130">Dans un navigateur web, accédez à l’adresse https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35f5e-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="35f5e-131">Dans le menu situé en haut de la page, sélectionnez **Éditeur Hive**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="35f5e-132">Cela affiche une page avec l'exemple de requête suivant.</span><span class="sxs-lookup"><span data-stu-id="35f5e-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="35f5e-133">Effacez l'exemple de requête et remplacez-le par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="35f5e-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="35f5e-134">Cliquez sur le bouton **Envoyer** .</span><span class="sxs-lookup"><span data-stu-id="35f5e-134">Select the **Submit** button.</span></span> <span data-ttu-id="35f5e-135">La section **Session de travail** en bas de la page affiche l'état de la requête.</span><span class="sxs-lookup"><span data-stu-id="35f5e-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="35f5e-136">Une fois que l'état passe à **Terminé**, sélectionnez le lien **Afficher les détails** pour afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="35f5e-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="35f5e-137">La **sortie de la tâche** doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="35f5e-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="35f5e-138">Utiliser l'interface utilisateur Tez</span><span class="sxs-lookup"><span data-stu-id="35f5e-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="35f5e-139">L'interface utilisateur Tez est seulement disponible à partir du bureau des nœuds principaux du cluster, donc vous devez utiliser le Bureau à distance pour vous connecter aux nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="35f5e-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="35f5e-140">Dans le [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35f5e-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="35f5e-141">En haut du panneau HDInsight, sélectionnez l’icône **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="35f5e-142">Le panneau du Bureau à distance s’affiche</span><span class="sxs-lookup"><span data-stu-id="35f5e-142">This will display the remote desktop blade</span></span>

    ![Icône Bureau à distance](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="35f5e-144">Dans le panneau du Bureau à distance, sélectionnez **Connexion** pour vous connecter au nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="35f5e-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="35f5e-145">Lorsque vous y êtes invité, utilisez le nom d'utilisateur et le mot de passe du Bureau à distance du cluster pour authentifier la connexion.</span><span class="sxs-lookup"><span data-stu-id="35f5e-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Icône Connexion Bureau à distance](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="35f5e-147">Si vous n'avez pas activé la connexion Bureau à distance, fournissez un nom d'utilisateur, un mot de passe et la date d'expiration, puis sélectionnez **Activer** pour activer le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="35f5e-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="35f5e-148">Une fois celui-ci activé, utilisez les étapes précédentes pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="35f5e-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="35f5e-149">Une fois connecté, ouvrez Internet Explorer sur le Bureau à distance, sélectionnez l'icône d'engrenage dans l’angle supérieur droit du navigateur, puis **Paramètres d’affichage de compatibilité**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="35f5e-150">En bas de la section **Paramètres d’affichage de compatibilité**, désactivez la case **Afficher les sites intranet dans Affichage de compatibilité** et **Utiliser les listes de compatibilité Microsoft**, puis sélectionnez **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="35f5e-151">Dans Internet Explorer, accédez à http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="35f5e-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="35f5e-152">L’interface utilisateur de Tez s’affiche</span><span class="sxs-lookup"><span data-stu-id="35f5e-152">This will display the Tez UI</span></span>

    ![Interface utilisateur Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="35f5e-154">Une fois l’interface utilisateur Tez chargée, vous voyez apparaître la liste des DAG en cours d’exécution ou qui ont été exécutés sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="35f5e-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="35f5e-155">La vue par défaut inclut le nom du DAG, l’ID, l’émetteur, l’état, l’heure de début, l’heure de fin, la durée, l’ID d’application et la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="35f5e-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="35f5e-156">Il est possible d’ajouter des colonnes à l’aide de l’icône d’engrenage à droite de la page.</span><span class="sxs-lookup"><span data-stu-id="35f5e-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="35f5e-157">Si vous ne voyez qu’une seule entrée, il s’agit de la requête que vous avez exécutée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="35f5e-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="35f5e-158">Si vous voyez plusieurs entrées, vous pouvez effectuer une recherche en entrant des critères dans les champs au-dessus du DAG, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="35f5e-159">Sélectionnez le **Nom du Dag** pour l’entrée DAG la plus récente.</span><span class="sxs-lookup"><span data-stu-id="35f5e-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="35f5e-160">Cette action permet d’afficher les informations sur le DAG, et offre la possibilité de télécharger un fichier compressé des fichiers JSON contenant des informations sur le DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![Détails du DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="35f5e-162">Au-dessus des **Détails du DAG** se trouvent plusieurs liens pouvant être utilisés pour afficher des informations sur le DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="35f5e-163">**Compteurs du DAG** permet d’afficher les informations de compteurs pour ce DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="35f5e-164">**Vue graphique** permet d’afficher une représentation graphique de ce DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="35f5e-165">**Tous les vertex** permet d’afficher une liste des vertex dans ce DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="35f5e-166">**Toutes les tâches** permet d’afficher une liste des tâches pour tous les vertex dans ce DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="35f5e-167">**Toutes les tentatives de tâches** permet d’afficher des informations sur les tentatives d’exécution de tâches pour ce DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="35f5e-168">Si vous parcourez les colonnes Vertex, Tâches et Tentatives de tâches, vous voyez des liens permettant d’afficher les **compteurs** et d’**afficher ou télécharger les journaux** pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="35f5e-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="35f5e-169">Si le travail a échoué, les détails du DAG affichent un état d’ÉCHEC, ainsi que des liens vers des informations sur la tâche ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="35f5e-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="35f5e-170">Des informations de diagnostic seront affichées sous les détails du DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="35f5e-171">Sélectionnez **Vue graphique**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-171">Select **Graphical View**.</span></span> <span data-ttu-id="35f5e-172">Cette action permet d’afficher une représentation graphique du DAG.</span><span class="sxs-lookup"><span data-stu-id="35f5e-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="35f5e-173">Dans cette vue, vous pouvez placer la souris sur chaque vertex pour afficher les informations le concernant.</span><span class="sxs-lookup"><span data-stu-id="35f5e-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Vue graphique](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="35f5e-175">Cliquez sur un vertex pour charger ses **Détails du vertex**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="35f5e-176">Cliquez sur le vertex **Map 1** pour afficher les détails de cet élément.</span><span class="sxs-lookup"><span data-stu-id="35f5e-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="35f5e-177">Sélectionnez **Confirmer** pour confirmer la navigation.</span><span class="sxs-lookup"><span data-stu-id="35f5e-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Détails](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="35f5e-179">Notez qu’en haut de la page, vous disposez maintenant de liens relatifs aux vertex et aux tâches.</span><span class="sxs-lookup"><span data-stu-id="35f5e-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="35f5e-180">Vous pouvez également accéder à cette page en retournant aux **Détails du DAG**, en sélectionnant **Détails du vertex**, puis le vertex **Map 1**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="35f5e-181">**Compteurs du vertex** permet d’afficher les informations de compteurs pour ce vertex.</span><span class="sxs-lookup"><span data-stu-id="35f5e-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="35f5e-182">**Tâches** permet d’afficher les tâches de ce vertex.</span><span class="sxs-lookup"><span data-stu-id="35f5e-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="35f5e-183">**Tentatives de tâches** permet d’afficher des informations sur les tentatives d’exécution de tâches pour ce vertex.</span><span class="sxs-lookup"><span data-stu-id="35f5e-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="35f5e-184">**Sources et récepteurs** permet d’afficher les sources et les récepteurs de données pour ce vertex.</span><span class="sxs-lookup"><span data-stu-id="35f5e-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="35f5e-185">Comme avec le menu précédent, vous pouvez parcourir les colonnes Tâches, Tentatives de tâche et Sources et récepteurs__ afin d’afficher des liens vers d’autres informations pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="35f5e-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="35f5e-186">Sélectionnez **Tâches**, puis sélectionnez l’élément nommé **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="35f5e-187">Cette action permet d’afficher les **détails de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="35f5e-188">À partir de cet écran, vous pouvez consulter les **compteurs de tâche** et les **tentatives de tâche**.</span><span class="sxs-lookup"><span data-stu-id="35f5e-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Détails de la tâche](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="35f5e-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35f5e-190">Next Steps</span></span>
<span data-ttu-id="35f5e-191">Maintenant que vous avez appris à utiliser la vue Tez, obtenez plus d’informations sur l’ [Utilisation de Hive dans HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="35f5e-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="35f5e-192">Pour plus d’informations techniques sur Tez, consultez la [page Tez sur Hortonworks](http://hortonworks.com/hadoop/tez/)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="35f5e-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
