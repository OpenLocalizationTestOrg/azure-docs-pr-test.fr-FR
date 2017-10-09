---
title: "aaaUse UI Tez hdinsight basés sur Windows - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Tez UI toodebug Tez travaux sur HDInsight de HDInsight basés sur Windows."
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="abe4a-103">Utilisez hello Tez UI toodebug Tez travaux sur HDInsight de basés sur Windows</span><span class="sxs-lookup"><span data-stu-id="abe4a-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="abe4a-104">Hello Tez UI est une page web qui peuvent être utilisés des travaux de toounderstand et de débogage qui utilisent Tez en tant que moteur d’exécution hello sur les clusters HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="abe4a-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="abe4a-105">Hello Tez UI vous permet de travail de hello toovisualize comme un graphique des éléments connectés, explorez chaque élément et extraire des statistiques et informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="abe4a-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abe4a-106">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Windows.</span><span class="sxs-lookup"><span data-stu-id="abe4a-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="abe4a-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="abe4a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="abe4a-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="abe4a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abe4a-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="abe4a-109">Prerequisites</span></span>
* <span data-ttu-id="abe4a-110">Un cluster HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="abe4a-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="abe4a-111">Pour plus d’informations sur la création d’un cluster, consultez [Prise en main de HDInsight sur Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="abe4a-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="abe4a-112">Hello Tez UI est disponible uniquement sur les clusters HDInsight de basés sur Windows créés après le 8 février 2016.</span><span class="sxs-lookup"><span data-stu-id="abe4a-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="abe4a-113">Un client Bureau à distance basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="abe4a-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="abe4a-114">Présentation de Tez</span><span class="sxs-lookup"><span data-stu-id="abe4a-114">Understanding Tez</span></span>
<span data-ttu-id="abe4a-115">Tez est une infrastructure extensible pour le traitement des données dans Hadoop plus rapide que le traitement MapReduce traditionnel.</span><span class="sxs-lookup"><span data-stu-id="abe4a-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="abe4a-116">Pour les clusters HDInsight de basés sur Windows, il est un moteur facultatif que vous pouvez activer pour la ruche à l’aide de hello commande suivante en tant que partie de votre requête Hive :</span><span class="sxs-lookup"><span data-stu-id="abe4a-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="abe4a-117">Lorsque le travail est soumis tooTez, il crée un dirigées acycliques graphique (DAG) qui décrit l’ordre de hello d’exécution des actions hello requis par le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="abe4a-118">Différentes actions sont appelées des sommets et exécuter une partie de hello travail global.</span><span class="sxs-lookup"><span data-stu-id="abe4a-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="abe4a-119">l’exécution réelle de Hello de travail hello décrite par un sommet est appelée une tâche et peut être répartie sur plusieurs nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="abe4a-120">Hello de présentation Tez UI</span><span class="sxs-lookup"><span data-stu-id="abe4a-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="abe4a-121">Hello Tez UI est qu'une page web fournit des informations sur les processus sont en cours d’exécution ou qui ont exécutaient précédemment à l’aide de Tez.</span><span class="sxs-lookup"><span data-stu-id="abe4a-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="abe4a-122">Il vous permet de tooview hello DAG généré par Tez, comment elle est répartie entre les clusters, compteurs telles que la mémoire utilisée par les tâches et les sommets et les informations d’erreur.</span><span class="sxs-lookup"><span data-stu-id="abe4a-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="abe4a-123">Il offre des informations utiles dans hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="abe4a-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="abe4a-124">Surveillance des processus longs, affichage hello la progression de la carte et réduire les tâches.</span><span class="sxs-lookup"><span data-stu-id="abe4a-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="abe4a-125">Analyse des données historiques pour les processus réussies ou échouées toolearn comment le traitement peut être amélioré ou en raison de l’échec.</span><span class="sxs-lookup"><span data-stu-id="abe4a-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="abe4a-126">Générer un DAG</span><span class="sxs-lookup"><span data-stu-id="abe4a-126">Generate a DAG</span></span>
<span data-ttu-id="abe4a-127">Hello Tez UI contiendra uniquement les données si une tâche qui utilise hello Tez moteur est en cours d’exécution ou a été exécuté dans hello passée.</span><span class="sxs-lookup"><span data-stu-id="abe4a-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="abe4a-128">Les requêtes Hive simples peuvent généralement être résolues sans utiliser Tez. Toutefois, Tez est généralement nécessaire pour les requêtes plus complexes destinées à filtrer, regrouper, classer, joindre, etc.</span><span class="sxs-lookup"><span data-stu-id="abe4a-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="abe4a-129">Utilisez hello suivant les étapes toorun une requête Hive qui s’exécute à l’aide de Tez.</span><span class="sxs-lookup"><span data-stu-id="abe4a-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="abe4a-130">Dans un navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** hello désigne votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abe4a-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="abe4a-131">Dans le menu de hello en hello haut hello, sélectionnez hello **éditeur Hive**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="abe4a-132">Cela affiche une page avec hello suivant l’exemple de requête.</span><span class="sxs-lookup"><span data-stu-id="abe4a-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="abe4a-133">Effacer la requête d’exemple hello et remplacez-le par suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="abe4a-134">Sélectionnez hello **Submit** bouton.</span><span class="sxs-lookup"><span data-stu-id="abe4a-134">Select hello **Submit** button.</span></span> <span data-ttu-id="abe4a-135">Hello **Session de travail** section bas hello de page de hello affichera hello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="abe4a-136">Une fois hello les changements d’état trop**terminé**, sélectionnez hello **afficher les détails** lier tooview hello résultats.</span><span class="sxs-lookup"><span data-stu-id="abe4a-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="abe4a-137">Hello **sortie des tâches** sont similaires toohello suivants :</span><span class="sxs-lookup"><span data-stu-id="abe4a-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="abe4a-138">Utilisez hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="abe4a-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="abe4a-139">Hello Tez UI est uniquement disponible à partir du bureau hello hello principal des nœuds de cluster, vous devez utiliser les nœuds principaux de toohello tooconnect Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="abe4a-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="abe4a-140">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abe4a-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="abe4a-141">À partir du haut hello du Panneau de HDInsight hello, sélectionnez hello **Bureau à distance** icône.</span><span class="sxs-lookup"><span data-stu-id="abe4a-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="abe4a-142">Panneau de bureau à distance hello s’affiche</span><span class="sxs-lookup"><span data-stu-id="abe4a-142">This will display hello remote desktop blade</span></span>

    ![Icône Bureau à distance](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="abe4a-144">Dans le panneau de bureau à distance hello, sélectionnez **Connect** nœud principal du cluster toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="abe4a-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="abe4a-145">Lorsque vous y êtes invité, utilisez hello cluster connexion Bureau à distance utilisateur nom et mot de passe tooauthenticate hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Icône Connexion Bureau à distance](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="abe4a-147">Si vous n’avez pas activé la connectivité Bureau à distance, fournissez un nom d’utilisateur, le mot de passe et la date d’expiration, puis sélectionnez **activer** tooenable Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="abe4a-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="abe4a-148">Une fois qu’elle a été activée, utilisez hello précédentes étapes tooconnect.</span><span class="sxs-lookup"><span data-stu-id="abe4a-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="abe4a-149">Une fois connecté, ouvrez Internet Explorer sur le Bureau à distance hello, icône d’engrenage sélectionnez hello dans hello coin supérieur droit navigateur hello, puis **paramètres d’affichage de compatibilité**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="abe4a-150">À partir du bas hello de **paramètres d’affichage de compatibilité**, désactivez hello case à cocher **afficher les sites intranet dans Affichage de compatibilité** et **listes de compatibilité d’utiliser Microsoft**, puis sélectionnez **fermer**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="abe4a-151">Dans Internet Explorer, accédez à toohttp://headnodehost:8188/tezui / #.</span><span class="sxs-lookup"><span data-stu-id="abe4a-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="abe4a-152">Cette action affiche hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="abe4a-152">This will display hello Tez UI</span></span>

    ![Interface utilisateur Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="abe4a-154">Lors du chargement de hello Tez UI, vous verrez une liste de décisionnels qui sont en cours d’exécution, ou qui ont été exécutés sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="abe4a-155">affichage par défaut de Hello inclut Bonjour Dag Name, Id, émetteur, état, l’heure de début, heure de fin, durée, ID d’Application et file d’attente.</span><span class="sxs-lookup"><span data-stu-id="abe4a-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="abe4a-156">Plus de colonnes peuvent être ajoutés à l’aide d’icône d’engrenage hello en hello à droite de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="abe4a-157">Si vous avez une seule entrée, il sera de requête hello que vous avez exécuté dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="abe4a-158">Si vous avez plusieurs entrées, vous pouvez rechercher en entrant les critères de recherche dans les champs hello ci-dessus hello décisionnels, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="abe4a-159">Sélectionnez hello **Dag Name** pour l’entrée de DAG hello plus récente.</span><span class="sxs-lookup"><span data-stu-id="abe4a-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="abe4a-160">Cela affiche des informations sur hello DAG, ainsi que toodownload d’option hello un fichier zip de fichiers JSON qui contiennent des informations sur hello DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Détails du DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="abe4a-162">Ci-dessus hello **DAG détails** plusieurs liens qui peuvent être utilisés toodisplay informations hello DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="abe4a-163">**Compteurs du DAG** permet d’afficher les informations de compteurs pour ce DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="abe4a-164">**Vue graphique** permet d’afficher une représentation graphique de ce DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="abe4a-165">**Tous les sommets** affiche une liste des sommets de hello dans cet DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="abe4a-166">**Toutes les tâches** affiche une liste de tâches hello pour tous les sommets dans cet DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="abe4a-167">**Tous les TaskAttempts** affiche des informations sur hello tente toorun tâches pour cet DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="abe4a-168">Si vous faites défiler l’affichage des colonnes hello pour les sommets, tâches et TaskAttempts, notez qu’il existe des liens tooview **compteurs** et **afficher ou télécharger les journaux** pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="abe4a-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="abe4a-169">S’il existe une erreur avec la tâche de hello, hello DAG détails affiche un état Échec, ainsi que de tooinformation de liens sur la tâche ayant échoué hello.</span><span class="sxs-lookup"><span data-stu-id="abe4a-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="abe4a-170">Informations de diagnostic seront affichera sous Détails de hello DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="abe4a-171">Sélectionnez **Vue graphique**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-171">Select **Graphical View**.</span></span> <span data-ttu-id="abe4a-172">Cela affiche une représentation graphique de hello DAG.</span><span class="sxs-lookup"><span data-stu-id="abe4a-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="abe4a-173">Vous pouvez placer la souris de hello sur chaque sommet dans hello vue toodisplay informations.</span><span class="sxs-lookup"><span data-stu-id="abe4a-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Vue graphique](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="abe4a-175">En cliquant sur un sommet chargera hello **détails sommets** pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="abe4a-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="abe4a-176">Cliquez sur hello **carte 1** détails toodisplay de sommets pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="abe4a-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="abe4a-177">Sélectionnez **confirmer** navigation de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="abe4a-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Détails](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="abe4a-179">Notez que vous disposez maintenant des liens en hello haut hello qui sont des tâches et toovertices connexes.</span><span class="sxs-lookup"><span data-stu-id="abe4a-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="abe4a-180">Vous pouvez également arriver à cette page en revenant trop**DAG détails**, en sélectionnant **détails de sommets**, puis en sélectionnant hello **1 de la carte** sommet.</span><span class="sxs-lookup"><span data-stu-id="abe4a-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="abe4a-181">**Compteurs du vertex** permet d’afficher les informations de compteurs pour ce vertex.</span><span class="sxs-lookup"><span data-stu-id="abe4a-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="abe4a-182">**Tâches** permet d’afficher les tâches de ce vertex.</span><span class="sxs-lookup"><span data-stu-id="abe4a-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="abe4a-183">**Tentatives de tâches** affiche des informations sur les tâches de toorun tentatives pour ce vertex.</span><span class="sxs-lookup"><span data-stu-id="abe4a-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="abe4a-184">**Sources et récepteurs** permet d’afficher les sources et les récepteurs de données pour ce vertex.</span><span class="sxs-lookup"><span data-stu-id="abe4a-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abe4a-185">Comme avec menu précédent de hello, vous pouvez faire défiler l’affichage des colonnes hello pour les tâches, les tentatives de tâche et les Sources & Sinks__ toodisplay lie toomore des informations pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="abe4a-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="abe4a-186">Sélectionnez **tâches**, et puis sélectionnez hello élément **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="abe4a-187">Cette action permet d’afficher les **détails de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="abe4a-188">À partir de cet écran, vous pouvez consulter les **compteurs de tâche** et les **tentatives de tâche**.</span><span class="sxs-lookup"><span data-stu-id="abe4a-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Détails de la tâche](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="abe4a-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="abe4a-190">Next Steps</span></span>
<span data-ttu-id="abe4a-191">Maintenant que vous avez appris comment toouse hello Tez afficher, en savoir plus sur [à l’aide de la ruche sur HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="abe4a-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="abe4a-192">Pour plus d’informations techniques sur Tez, consultez hello [page Tez sur Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="abe4a-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
