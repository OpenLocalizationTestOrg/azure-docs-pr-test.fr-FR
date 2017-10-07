---
title: "aaaDeploy et gérer les topologies d’Apache Storm sur HDInsight de basés sur Linux | Documents Microsoft"
description: "Découvrez comment toodeploy, surveiller et gérer des topologies de Apache Storm à l’aide de hello du tableau de bord Storm sur HDInsight de basés sur Linux. Utilisez les outils Hadoop pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="65452-104">Déploiement et gestion des topologies Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="65452-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="65452-105">Dans ce document, principes hello de gérer et surveiller les topologies Storm sur Storm sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65452-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65452-106">Hello étapes décrites dans cet article nécessitent une tempête basés sur Linux sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65452-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="65452-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="65452-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="65452-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="65452-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="65452-109">Pour plus d’informations sur le déploiement et la surveillance des topologies sur HDInsight Windows, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="65452-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="65452-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="65452-110">Prerequisites</span></span>

* <span data-ttu-id="65452-111">**Un cluster Storm Linux sur HDInsight**: consultez [Prise en main d’Apache Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) pour connaître les étapes de création d’un cluster</span><span class="sxs-lookup"><span data-stu-id="65452-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="65452-112">(Facultatif) **Des connaissances en SSH et SCP** : pour plus d’informations, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="65452-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="65452-113">(Facultatif) **Visual Studio**: Kit de développement logiciel Azure 2.5.1 ou plus récent et hello Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65452-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="65452-114">Pour plus d’informations, consultez [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) (Prise en main de Data Lake Tools pour Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="65452-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="65452-115">Une des hello versions de Visual Studio suivantes :</span><span class="sxs-lookup"><span data-stu-id="65452-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="65452-116">Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="65452-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="65452-117">Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="65452-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="65452-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="65452-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="65452-119">Visual Studio 2015 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="65452-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="65452-120">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="65452-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="65452-121">Data Lake Tools pour Visual Studio 2017 sont installés dans le cadre de hello la charge de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="65452-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="65452-122">Soumettre une topologie : Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65452-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="65452-123">Hello HDInsight outils peut être utilisé toosubmit c# ou hybride topologies tooyour cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="65452-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="65452-124">Hello suit utilisent un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="65452-124">hello following steps use a sample application.</span></span> <span data-ttu-id="65452-125">Pour plus d’informations sur la création de vos propres topologies à l’aide des outils de HDInsight hello, consultez [C# développer des topologies à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="65452-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="65452-126">Si vous n’avez pas déjà installé version la plus récente des outils de Data Lake hello hello pour Visual Studio, consultez [prise en main Data Lake Tools pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65452-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="65452-127">Hello Data Lake Tools pour Visual Studio ont été précédemment appelé hello HDInsight Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65452-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="65452-128">Data Lake Tools pour Visual Studio sont inclus dans hello __la charge de travail Azure__ pour Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="65452-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="65452-129">Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="65452-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="65452-130">Bonjour **nouveau projet** boîte de dialogue, développez **installé** > **modèles**, puis sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="65452-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="65452-131">Dans la liste hello des modèles, sélectionnez **Storm exemple**.</span><span class="sxs-lookup"><span data-stu-id="65452-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="65452-132">Bas hello de boîte de dialogue hello, tapez un nom pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="65452-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="65452-134">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="65452-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="65452-135">Si vous y êtes invité, entrez les informations d’identification de connexion hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="65452-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="65452-136">Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65452-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="65452-137">Sélectionnez votre Storm sur le cluster HDInsight à partir de hello **Cluster Storm** liste déroulante et sélectionnez **Submit**.</span><span class="sxs-lookup"><span data-stu-id="65452-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="65452-138">Vous pouvez surveiller si l’envoi de hello réussit à l’aide de hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="65452-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="65452-139">Envoyer une topologie : SSH et hello renverser commande</span><span class="sxs-lookup"><span data-stu-id="65452-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="65452-140">Utiliser SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="65452-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="65452-141">Remplacez **nom d’utilisateur** nom hello de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="65452-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="65452-142">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="65452-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="65452-143">Pour plus d’informations sur l’utilisation de SSH tooconnect tooyour HDInsight de cluster, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="65452-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="65452-144">Utilisez hello suivant commande toostart un exemple de topologie :</span><span class="sxs-lookup"><span data-stu-id="65452-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="65452-145">Cette commande démarre hello exemple WordCount de topologie de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="65452-146">Cette topologie générer de façon aléatoire les phrases et les occurrences de hello de nombre de chaque mot dans les phrases hello.</span><span class="sxs-lookup"><span data-stu-id="65452-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="65452-147">Lors de la soumission cluster toohello de topologie, vous devez d’abord copier le fichier jar hello contenant le cluster de hello avant d’utiliser hello `storm` commande.</span><span class="sxs-lookup"><span data-stu-id="65452-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="65452-148">toocopy hello toohello de fichiers, vous pouvez utiliser hello `scp` commande.</span><span class="sxs-lookup"><span data-stu-id="65452-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="65452-149">Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="65452-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="65452-150">exemple WordCount de Hello et des autres exemples de starter storm, figurent déjà sur votre cluster à `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="65452-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="65452-151">Soumettre une topologie : par programme</span><span class="sxs-lookup"><span data-stu-id="65452-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="65452-152">Vous pouvez par programmation déployer un tooStorm topologie sur HDInsight en communiquant avec hello service Nimbus hébergé dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="65452-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="65452-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) fournit un exemple d’application Java qui montre comment toodeploy et démarrer une topologie via le service de Nimbus de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="65452-154">Surveiller et gérer : Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65452-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="65452-155">Lorsqu’une topologie a été envoyée à l’aide de Visual Studio, hello **Storm Topologies** permet d’afficher de hello cluster apparaît.</span><span class="sxs-lookup"><span data-stu-id="65452-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="65452-156">Sélectionnez la topologie de hello dans hello liste tooview informations hello topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="65452-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![Visual Studio Monitor](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="65452-158">Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs** en développant **Azure** > **HDInsight**, puis en cliquant avec le bouton droit sur le cluster HDInsight et en sélectionnant **Affichage des topologies Storm**.</span><span class="sxs-lookup"><span data-stu-id="65452-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="65452-159">Sélectionnez la forme de hello pour hello becs verseurs amovibles ou boulons tooview d’informations sur ces composants.</span><span class="sxs-lookup"><span data-stu-id="65452-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="65452-160">Une nouvelle fenêtre s’ouvre pour chaque élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="65452-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="65452-161">Désactivation et réactivation</span><span class="sxs-lookup"><span data-stu-id="65452-161">Deactivate and reactivate</span></span>

<span data-ttu-id="65452-162">La désactivation d’une topologie la met en pause jusqu’à ce qu’elle soit arrêtée ou réactivée.</span><span class="sxs-lookup"><span data-stu-id="65452-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="65452-163">tooperform ces opérations, utilisez hello __Deactivate__ et __réactiver__ boutons haut hello hello __récapitulatif de la topologie__.</span><span class="sxs-lookup"><span data-stu-id="65452-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="65452-164">Rééquilibrage</span><span class="sxs-lookup"><span data-stu-id="65452-164">Rebalance</span></span>

<span data-ttu-id="65452-165">Rééquilibrage une topologie permet de parallélisme de hello hello système toorevise de topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="65452-166">Par exemple, si vous avez redimensionné hello cluster tooadd autres notes, rééquilibrage permet une topologie de nouveaux nœuds de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="65452-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="65452-167">toorebalance une topologie, utilisez hello __rééquilibrer__ bouton haut hello hello __récapitulatif de la topologie__.</span><span class="sxs-lookup"><span data-stu-id="65452-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="65452-168">Tout d’abord le rééquilibrage une topologie désactive la topologie de hello, répartit uniformément les travailleurs sur le cluster de hello, puis enfin retourne toohello état de la topologie hello qu'il se trouvait avant le rééquilibrage s’est produite.</span><span class="sxs-lookup"><span data-stu-id="65452-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="65452-169">Par conséquent, si la topologie de hello était active, elle redevient actif.</span><span class="sxs-lookup"><span data-stu-id="65452-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="65452-170">Si elle était désactivée, elle reste désactivée.</span><span class="sxs-lookup"><span data-stu-id="65452-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="65452-171">Supprimer une topologie</span><span class="sxs-lookup"><span data-stu-id="65452-171">Kill a topology</span></span>

<span data-ttu-id="65452-172">Les topologies Storm poursuivre l’exécution jusqu'à ce qu’ils sont arrêtés ou cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="65452-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="65452-173">toostop une topologie, utilisez hello __Kill__ bouton haut hello hello __récapitulatif de la topologie__.</span><span class="sxs-lookup"><span data-stu-id="65452-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="65452-174">Surveiller et gérer : SSH et hello renverser commande</span><span class="sxs-lookup"><span data-stu-id="65452-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="65452-175">Hello `storm` utilitaire vous permet de toowork avec les topologies en cours d’exécution à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="65452-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="65452-176">Pour obtenir la liste complète des commandes, utilisez `storm -h` .</span><span class="sxs-lookup"><span data-stu-id="65452-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="65452-177">Liste de toutes les topologies</span><span class="sxs-lookup"><span data-stu-id="65452-177">List topologies</span></span>

<span data-ttu-id="65452-178">Utilisez hello suivant toolist de commande toutes les topologies en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="65452-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="65452-179">Cette commande retourne toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="65452-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="65452-180">Désactivation et réactivation</span><span class="sxs-lookup"><span data-stu-id="65452-180">Deactivate and reactivate</span></span>

<span data-ttu-id="65452-181">La désactivation d’une topologie la met en pause jusqu’à ce qu’elle soit arrêtée ou réactivée.</span><span class="sxs-lookup"><span data-stu-id="65452-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="65452-182">Utilisez hello suivant commande toodeactivate et réactiver :</span><span class="sxs-lookup"><span data-stu-id="65452-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="65452-183">Arrêt d’une topologie en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="65452-183">Kill a running topology</span></span>

<span data-ttu-id="65452-184">Les topologies Storm, une fois démarrées, continuent leur exécution jusqu’à ce qu’elles soient arrêtées.</span><span class="sxs-lookup"><span data-stu-id="65452-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="65452-185">toostop une topologie, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65452-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="65452-186">Rééquilibrage</span><span class="sxs-lookup"><span data-stu-id="65452-186">Rebalance</span></span>

<span data-ttu-id="65452-187">Rééquilibrage une topologie permet de parallélisme de hello hello système toorevise de topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="65452-188">Par exemple, si vous avez redimensionné hello cluster tooadd autres notes, rééquilibrage permet une topologie de nouveaux nœuds de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="65452-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="65452-189">Tout d’abord le rééquilibrage une topologie désactive la topologie de hello, répartit uniformément les travailleurs sur le cluster de hello, puis enfin retourne toohello état de la topologie hello qu'il se trouvait avant le rééquilibrage s’est produite.</span><span class="sxs-lookup"><span data-stu-id="65452-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="65452-190">Par conséquent, si la topologie de hello était active, elle redevient actif.</span><span class="sxs-lookup"><span data-stu-id="65452-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="65452-191">Si elle était désactivée, elle reste désactivée.</span><span class="sxs-lookup"><span data-stu-id="65452-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="65452-192">Surveiller et gérer : interface utilisateur de Storm</span><span class="sxs-lookup"><span data-stu-id="65452-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="65452-193">Bonjour Storm UI fournit une interface web pour l’utilisation des topologies en cours d’exécution et est inclus dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65452-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="65452-194">tooview hello Storm UI, utilisez un tooopen de navigateur web **https://CLUSTERNAME.azurehdinsight.net/stormui**, où **CLUSTERNAME** est le nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="65452-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="65452-195">Si vous êtes invité tooprovide un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster hello (admin) et un mot de passe que vous avez utilisé lors des cluster hello création.</span><span class="sxs-lookup"><span data-stu-id="65452-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="65452-196">Page principale</span><span class="sxs-lookup"><span data-stu-id="65452-196">Main page</span></span>

<span data-ttu-id="65452-197">page principale de Hello Hello Storm UI fournit hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="65452-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="65452-198">**Résumé du cluster**: informations de base sur le cluster de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="65452-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="65452-199">**Résumé de la topologie**: une liste des topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="65452-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="65452-200">Utilisez les liens hello tooview de cette section plus d’informations sur les topologies spécifiques.</span><span class="sxs-lookup"><span data-stu-id="65452-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="65452-201">**Résumé de superviseur**: plus d’informations sur le superviseur de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="65452-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="65452-202">**Configuration de Nimbus**: configuration Nimbus pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="65452-203">Résumé de la topologie</span><span class="sxs-lookup"><span data-stu-id="65452-203">Topology summary</span></span>

<span data-ttu-id="65452-204">Sélection d’un lien à partir de hello **récapitulatif de la topologie** section affiche hello informations sur la topologie de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="65452-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="65452-205">**Résumé de la topologie**: informations de base sur la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="65452-206">**Actions de topologie**: actions de gestion que vous pouvez effectuer pour la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="65452-207">**Activer**: reprend le traitement d’une topologie arrêtée.</span><span class="sxs-lookup"><span data-stu-id="65452-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="65452-208">**Désactiver**: suspend une topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="65452-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="65452-209">**Rééquilibrer**: ajuste le parallélisme hello de topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="65452-210">Vous devez rééquilibrer les topologies en cours d’exécution une fois que vous avez modifié le nombre de hello de nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="65452-211">Cette opération permet de hello topologie tooadjust parallélisme toocompensate pour hello augmenté ou diminué le nombre de nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="65452-212">Pour plus d’informations, consultez <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">présentation parallélisme hello d’une topologie de Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="65452-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="65452-213">**KILL**: met fin à une topologie Storm après hello spécifié le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="65452-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="65452-214">**Statistiques de topologie**: statistiques sur la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="65452-215">tooset hello laps de temps pour hello restant entrées sur la page de hello, utilisez les liens hello hello **fenêtre** colonne.</span><span class="sxs-lookup"><span data-stu-id="65452-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="65452-216">**Becs verseurs amovibles**: hello becs verseurs utilisés par la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="65452-217">Utilisez les liens hello tooview de cette section plus d’informations sur becs verseurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="65452-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="65452-218">**Boulons**: hello boulons utilisés par la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="65452-219">Utilisez les liens hello tooview de cette section plus d’informations sur les boulons spécifiques.</span><span class="sxs-lookup"><span data-stu-id="65452-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="65452-220">**Configuration de la topologie**: configuration hello de topologie de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="65452-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="65452-221">Résumé relatif aux spouts et aux bolts</span><span class="sxs-lookup"><span data-stu-id="65452-221">Spout and Bolt summary</span></span>

<span data-ttu-id="65452-222">En sélectionnant un bec de hello **becs verseurs amovibles** ou **boulons** sections affiche hello suit les informations d’élément de hello sélectionné :</span><span class="sxs-lookup"><span data-stu-id="65452-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="65452-223">**Résumé des composants**: informations de base sur bec de hello ou éclair.</span><span class="sxs-lookup"><span data-stu-id="65452-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="65452-224">**BEC/éclair statistiques**: statistiques sur hello bec ou boulon.</span><span class="sxs-lookup"><span data-stu-id="65452-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="65452-225">tooset hello laps de temps pour hello restant entrées sur la page de hello, utilisez les liens hello hello **fenêtre** colonne.</span><span class="sxs-lookup"><span data-stu-id="65452-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="65452-226">**D’entrée statistiques** (boulon uniquement) : flux consommées par un éclair de hello d’entrée le plus d’informations sur hello.</span><span class="sxs-lookup"><span data-stu-id="65452-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="65452-227">**Statistiques de sortie**: plus d’informations sur les flux hello émis par ce bec ou boulon.</span><span class="sxs-lookup"><span data-stu-id="65452-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="65452-228">**Les exécuteurs**: informations sur les instances de hello de bec de hello ou éclair.</span><span class="sxs-lookup"><span data-stu-id="65452-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="65452-229">Sélectionnez hello **Port** entrée pour un tooview spécifique de l’exécuteur un journal d’informations de diagnostic généré pour cette instance.</span><span class="sxs-lookup"><span data-stu-id="65452-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="65452-230">**Erreurs**: les informations d’erreur pour ce spout ou ce bolt.</span><span class="sxs-lookup"><span data-stu-id="65452-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="65452-231">Surveiller et gérer : API REST</span><span class="sxs-lookup"><span data-stu-id="65452-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="65452-232">Hello Storm UI repose sur hello API REST, afin de pouvoir effectuer similaires de gestion et de la fonctionnalité d’analyse à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="65452-233">Vous pouvez utiliser des outils personnalisés hello API REST toocreate pour gérer et surveiller les topologies de Storm.</span><span class="sxs-lookup"><span data-stu-id="65452-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="65452-234">Pour plus d’informations, consultez la rubrique [API REST de l’interface utilisateur Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="65452-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="65452-235">Hello informations suivantes sont spécifiques toousing hello API REST avec Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65452-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65452-236">Hello Storm REST API n’est pas disponible publiquement hello internet et doit être accessible à l’aide d’un SSH tunnel toohello HDInsight nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="65452-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="65452-237">Pour plus d’informations sur la création et à l’aide d’un tunnel SSH, consultez [tooaccess utiliser SSH Tunneling Ambari web de l’interface utilisateur, ResourceManager, JobHistory, NameNode, Oozie et autres interfaces utilisateur web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="65452-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="65452-238">URI de base</span><span class="sxs-lookup"><span data-stu-id="65452-238">Base URI</span></span>

<span data-ttu-id="65452-239">Bonjour URI de base pour l’API REST de hello sur les clusters HDInsight de basés sur Linux est disponible sur le nœud principal hello **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="65452-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="65452-240">nom de domaine Hello de nœud principal de hello est généré au cours de la création du cluster et n’est pas statique.</span><span class="sxs-lookup"><span data-stu-id="65452-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="65452-241">Vous pouvez trouver le nom de domaine complet (FQDN) hello pour le nœud principal du cluster hello de plusieurs façons différentes :</span><span class="sxs-lookup"><span data-stu-id="65452-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="65452-242">**À partir d’une session SSH**: utiliser la commande hello `headnode -f` à partir d’un cluster de toohello session SSH.</span><span class="sxs-lookup"><span data-stu-id="65452-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="65452-243">**À partir de Ambari Web**: sélectionnez **Services** de hello en haut de page de hello, puis sélectionnez **Storm**.</span><span class="sxs-lookup"><span data-stu-id="65452-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="65452-244">À partir de hello **Résumé** onglet, sélectionnez **Storm UI Server**.</span><span class="sxs-lookup"><span data-stu-id="65452-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="65452-245">Hello, nom de domaine complet du nœud de hello hello Storm UI et l’API REST est en cours d’exécution est en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="65452-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="65452-246">**À partir de l’API REST de Ambari**: utiliser la commande hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve plus d’informations sur le nœud hello hello Storm UI et l’API REST sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="65452-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="65452-247">Remplacez **mot de passe** avec le mot de passe administrateur hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="65452-248">Remplacez **CLUSTERNAME** avec le nom du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="65452-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="65452-249">Dans la réponse de hello, écriture de « host_name » hello contient hello nom de domaine complet du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="65452-250">Authentification</span><span class="sxs-lookup"><span data-stu-id="65452-250">Authentication</span></span>

<span data-ttu-id="65452-251">Toohello demandes API REST doivent utiliser **l’authentification de base**, de sorte que vous utilisez le nom du cluster hello HDInsight administrateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="65452-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="65452-252">Étant donné que l’authentification de base est envoyée à l’aide de texte en clair, vous devez **toujours** utiliser les communications HTTPS toosecure avec cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="65452-253">Valeurs de retour</span><span class="sxs-lookup"><span data-stu-id="65452-253">Return values</span></span>

<span data-ttu-id="65452-254">Informations qui sont retournées à partir de hello API REST peuvent uniquement être utilisable à partir de cluster de hello ou ordinateurs virtuels sur hello même réseau virtuel Azure en tant que cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65452-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="65452-255">Par exemple, nom de domaine complet de hello (FQDN) retournée pour les serveurs soigneur n'est pas accessible à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="65452-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65452-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65452-256">Next Steps</span></span>

<span data-ttu-id="65452-257">Maintenant que vous avez appris comment topologies toodeploy et le moniteur à l’aide de hello Storm le tableau de bord, découvrez comment trop[basée sur Java de développer des topologies, à l’aide de Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="65452-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="65452-258">Pour accéder à une liste d’exemples supplémentaires de topologies, consultez la rubrique [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="65452-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
