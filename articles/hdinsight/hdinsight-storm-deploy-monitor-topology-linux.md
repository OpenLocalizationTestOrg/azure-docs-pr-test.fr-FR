---
title: "Déploiement et gestion de topologies Apache Storm sur HDInsight basé sur Linux | Microsoft Docs"
description: "Apprenez à déployer, surveiller et gérer des topologies Apache Storm à l’aide du tableau de bord Storm sur HDInsight basé sur Linux. Utilisez les outils Hadoop pour Visual Studio."
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="3ad59-104">Déploiement et gestion des topologies Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3ad59-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="3ad59-105">Ce document présente les principes fondamentaux de la gestion et de la surveillance des topologies Storm qui s’exécutent sur des clusters Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ad59-106">Les étapes décrites dans cet article nécessitent un cluster Storm Linux sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="3ad59-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="3ad59-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3ad59-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3ad59-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="3ad59-109">Pour plus d’informations sur le déploiement et la surveillance des topologies sur HDInsight Windows, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="3ad59-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3ad59-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3ad59-110">Prerequisites</span></span>

* <span data-ttu-id="3ad59-111">**Un cluster Storm Linux sur HDInsight**: consultez [Prise en main d’Apache Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) pour connaître les étapes de création d’un cluster</span><span class="sxs-lookup"><span data-stu-id="3ad59-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="3ad59-112">(Facultatif) **Des connaissances en SSH et SCP** : pour plus d’informations, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3ad59-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="3ad59-113">(Facultatif) Pour **Visual Studio** : le Kit de développement logiciel (SDK) Azure 2.5.1 ou une version ultérieure et Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ad59-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="3ad59-114">Pour plus d’informations, consultez [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) (Prise en main de Data Lake Tools pour Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="3ad59-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="3ad59-115">L’une des versions suivantes de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="3ad59-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="3ad59-116">Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="3ad59-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="3ad59-117">Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="3ad59-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="3ad59-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3ad59-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="3ad59-119">Visual Studio 2015 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="3ad59-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="3ad59-120">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="3ad59-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="3ad59-121">Data Lake Tools pour Visual Studio 2017 est installé avec la charge de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad59-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="3ad59-122">Soumettre une topologie : Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ad59-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="3ad59-123">Les outils HDInsight permettent de soumettre des topologies C# ou hybrides à votre cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="3ad59-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="3ad59-124">La procédure suivante utilise un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="3ad59-124">The following steps use a sample application.</span></span> <span data-ttu-id="3ad59-125">Pour plus d’informations sur la création de vos propres topologies à l’aide des outils HDInsight, consultez [Développement de topologies C# à l’aide des outils HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3ad59-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="3ad59-126">Si vous n’avez pas encore installé la dernière version de Data Lake Tools pour Visual Studio, consultez [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) (Prise en main de Data Lake Tools pour Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="3ad59-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ad59-127">Data Lake Tools pour Visual Studio est le nouveau nom des outils HDInsight pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ad59-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="3ad59-128">Data Lake Tools pour Visual Studio est inclus dans la __charge de travail Azure__ pour Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3ad59-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="3ad59-129">Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="3ad59-130">Dans la boîte de dialogue **Nouveau projet**, développez **Installé** > **Modèles**, puis sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="3ad59-131">Dans la liste des modèles, sélectionnez **Exemple Storm**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="3ad59-132">En bas de la boîte de dialogue, entrez un nom pour l’application.</span><span class="sxs-lookup"><span data-stu-id="3ad59-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="3ad59-134">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet, puis sélectionnez **Envoyer à Storm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3ad59-135">Si vous y êtes invité, entrez les informations d’identification de connexion pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad59-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="3ad59-136">Si vous disposez de plusieurs abonnements, connectez-vous à celui qui contient votre cluster Storm dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="3ad59-137">Sélectionnez votre Storm sur le cluster HDInsight dans la liste déroulante **Cluster Storm**, puis sélectionnez **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="3ad59-138">Vous pouvez contrôler si l’envoi a bien été effectué à l’aide de la fenêtre **Sortie** .</span><span class="sxs-lookup"><span data-stu-id="3ad59-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="3ad59-139">Soumettre une topologie : SSH et la commande Storm</span><span class="sxs-lookup"><span data-stu-id="3ad59-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="3ad59-140">Utilisez SSH pour vous connecter au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="3ad59-141">Remplacez **USERNAME** par le nom de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="3ad59-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="3ad59-142">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="3ad59-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="3ad59-143">Pour plus d’informations sur l’utilisation de SSH pour se connecter à votre cluster HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3ad59-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3ad59-144">Utilisez la commande suivante pour démarrer un exemple de topologie :</span><span class="sxs-lookup"><span data-stu-id="3ad59-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="3ad59-145">Cette commande démarre l’exemple de topologie WordCount sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="3ad59-146">Cette topologie va générer des phrases de manière aléatoire et compter les occurrences de chaque mot dans ces phrases.</span><span class="sxs-lookup"><span data-stu-id="3ad59-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3ad59-147">Pendant l’envoi de la topologie au cluster, vous devez d’abord copier le fichier jar contenant le cluster avant d’utiliser la commande `storm`.</span><span class="sxs-lookup"><span data-stu-id="3ad59-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="3ad59-148">Vous pouvez utiliser la commande `scp` pour copier le fichier sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="3ad59-149">Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="3ad59-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="3ad59-150">L’exemple WordCount et d’autres exemples de Storm Starter sont déjà inclus dans votre cluster sous `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="3ad59-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="3ad59-151">Soumettre une topologie : par programme</span><span class="sxs-lookup"><span data-stu-id="3ad59-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="3ad59-152">Vous pouvez, par programmation, déployer une topologie vers Storm sur HDInsight en communiquant avec le service Nimbus hébergé dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="3ad59-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) fournit un exemple d’application Java qui montre comment déployer et démarrer une topologie via le service Nimbus.</span><span class="sxs-lookup"><span data-stu-id="3ad59-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="3ad59-154">Surveiller et gérer : Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ad59-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="3ad59-155">Lorsqu’une topologie a été envoyée avec succès à l’aide de Visual Studio, la vue **Topologies Storm** des clusters s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3ad59-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="3ad59-156">Sélectionnez la topologie à partir de la liste pour afficher des informations sur la topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3ad59-156">Select the topology from the list to view information about the running topology.</span></span>

![Visual Studio Monitor](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="3ad59-158">Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs** en développant **Azure** > **HDInsight**, puis en cliquant avec le bouton droit sur le cluster HDInsight et en sélectionnant **Affichage des topologies Storm**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="3ad59-159">Sélectionnez la forme des spouts et bolts pour afficher des informations sur ces composants.</span><span class="sxs-lookup"><span data-stu-id="3ad59-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="3ad59-160">Une nouvelle fenêtre s’ouvre pour chaque élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3ad59-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="3ad59-161">Désactivation et réactivation</span><span class="sxs-lookup"><span data-stu-id="3ad59-161">Deactivate and reactivate</span></span>

<span data-ttu-id="3ad59-162">La désactivation d’une topologie la met en pause jusqu’à ce qu’elle soit arrêtée ou réactivée.</span><span class="sxs-lookup"><span data-stu-id="3ad59-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="3ad59-163">Pour effectuer ces opérations, utilisez les boutons __Désactiver__ et __Réactiver__ en haut de la fenêtre __Résumé de la topologie__.</span><span class="sxs-lookup"><span data-stu-id="3ad59-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="3ad59-164">Rééquilibrage</span><span class="sxs-lookup"><span data-stu-id="3ad59-164">Rebalance</span></span>

<span data-ttu-id="3ad59-165">Le rééquilibrage d’une topologie permet au système de réviser le parallélisme de la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="3ad59-166">Par exemple, si vous avez redimensionné le cluster pour ajouter plus de nœuds, le rééquilibrage permet à une topologie d’identifier les nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="3ad59-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="3ad59-167">Pour rééquilibrer une topologie, utilisez le bouton __Rééquilibrer__ en haut de la fenêtre __Résumé de la topologie__.</span><span class="sxs-lookup"><span data-stu-id="3ad59-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="3ad59-168">Le rééquilibrage d’une topologie désactive d’abord la topologie, puis redistribue les workers uniformément sur le cluster avant de rétablir la topologie dans l’état où elle se trouvait avant le rééquilibrage.</span><span class="sxs-lookup"><span data-stu-id="3ad59-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="3ad59-169">Par conséquent, si la topologie était active, elle redevient active.</span><span class="sxs-lookup"><span data-stu-id="3ad59-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="3ad59-170">Si elle était désactivée, elle reste désactivée.</span><span class="sxs-lookup"><span data-stu-id="3ad59-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="3ad59-171">Supprimer une topologie</span><span class="sxs-lookup"><span data-stu-id="3ad59-171">Kill a topology</span></span>

<span data-ttu-id="3ad59-172">Les topologies Storm poursuivent leur exécution jusqu'à ce qu'elles soient arrêtées ou que le cluster soit supprimé.</span><span class="sxs-lookup"><span data-stu-id="3ad59-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="3ad59-173">Pour supprimer une topologie, utilisez le bouton __Supprimer__ en haut de la fenêtre __Résumé de la topologie__.</span><span class="sxs-lookup"><span data-stu-id="3ad59-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="3ad59-174">Surveiller et gérer : SSH et la commande Storm</span><span class="sxs-lookup"><span data-stu-id="3ad59-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="3ad59-175">L’utilitaire `storm` vous permet d’utiliser des topologies en cours d’exécution à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="3ad59-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="3ad59-176">Pour obtenir la liste complète des commandes, utilisez `storm -h` .</span><span class="sxs-lookup"><span data-stu-id="3ad59-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="3ad59-177">Liste de toutes les topologies</span><span class="sxs-lookup"><span data-stu-id="3ad59-177">List topologies</span></span>

<span data-ttu-id="3ad59-178">Utilisez la commande suivante pour répertorier toutes les topologies en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="3ad59-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="3ad59-179">Cette commande renvoie des informations semblables au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="3ad59-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="3ad59-180">Désactivation et réactivation</span><span class="sxs-lookup"><span data-stu-id="3ad59-180">Deactivate and reactivate</span></span>

<span data-ttu-id="3ad59-181">La désactivation d’une topologie la met en pause jusqu’à ce qu’elle soit arrêtée ou réactivée.</span><span class="sxs-lookup"><span data-stu-id="3ad59-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="3ad59-182">Utilisez la commande suivante pour désactiver et réactiver une topologie :</span><span class="sxs-lookup"><span data-stu-id="3ad59-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="3ad59-183">Arrêt d’une topologie en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="3ad59-183">Kill a running topology</span></span>

<span data-ttu-id="3ad59-184">Les topologies Storm, une fois démarrées, continuent leur exécution jusqu’à ce qu’elles soient arrêtées.</span><span class="sxs-lookup"><span data-stu-id="3ad59-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="3ad59-185">Pour ce faire, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3ad59-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="3ad59-186">Rééquilibrage</span><span class="sxs-lookup"><span data-stu-id="3ad59-186">Rebalance</span></span>

<span data-ttu-id="3ad59-187">Le rééquilibrage d’une topologie permet au système de réviser le parallélisme de la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="3ad59-188">Par exemple, si vous avez redimensionné le cluster pour ajouter plus de nœuds, le rééquilibrage permet à une topologie d’identifier les nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="3ad59-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="3ad59-189">Le rééquilibrage d’une topologie désactive d’abord la topologie, puis redistribue les workers uniformément sur le cluster avant de rétablir la topologie dans l’état où elle se trouvait avant le rééquilibrage.</span><span class="sxs-lookup"><span data-stu-id="3ad59-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="3ad59-190">Par conséquent, si la topologie était active, elle redevient active.</span><span class="sxs-lookup"><span data-stu-id="3ad59-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="3ad59-191">Si elle était désactivée, elle reste désactivée.</span><span class="sxs-lookup"><span data-stu-id="3ad59-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="3ad59-192">Surveiller et gérer : interface utilisateur de Storm</span><span class="sxs-lookup"><span data-stu-id="3ad59-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="3ad59-193">L’interface utilisateur Storm fournit une interface web incluse dans votre cluster HDInsight pour utiliser les topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3ad59-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="3ad59-194">Pour afficher l’interface utilisateur Storm, ouvrez un navigateur web sur l’adresse **https://CLUSTERNAME.azurehdinsight.net/stormui**, où **CLUSTERNAME** est le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad59-195">Si vous êtes invité à fournir un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster (admin) et le mot de passe que vous avez utilisé pour la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="3ad59-196">Page principale</span><span class="sxs-lookup"><span data-stu-id="3ad59-196">Main page</span></span>

<span data-ttu-id="3ad59-197">La page principale de l’interface utilisateur de Storm fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ad59-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="3ad59-198">**Résumé du cluster**: des informations de base sur le cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="3ad59-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="3ad59-199">**Résumé de la topologie**: une liste des topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3ad59-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="3ad59-200">Utilisez les liens de cette section pour afficher plus d’informations sur les topologies spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3ad59-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="3ad59-201">**Résumé du superviseur**: des informations sur le superviseur Storm.</span><span class="sxs-lookup"><span data-stu-id="3ad59-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="3ad59-202">**Configuration Nimbus**: configuration Nimbus du cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="3ad59-203">Résumé de la topologie</span><span class="sxs-lookup"><span data-stu-id="3ad59-203">Topology summary</span></span>

<span data-ttu-id="3ad59-204">La sélection d’un lien de la section **Résumé de la topologie** affiche les informations suivantes sur la topologie :</span><span class="sxs-lookup"><span data-stu-id="3ad59-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="3ad59-205">**Résumé de la topologie**:des informations de base sur la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="3ad59-206">**Actions de la topologie**: les actions de gestion que vous pouvez effectuer sur la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="3ad59-207">**Activer**: reprend le traitement d’une topologie arrêtée.</span><span class="sxs-lookup"><span data-stu-id="3ad59-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="3ad59-208">**Désactiver**: suspend une topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3ad59-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="3ad59-209">**Rééquilibrer**: ajuste le parallélisme de la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="3ad59-210">Il convient de rééquilibrer les topologies en cours d’exécution après avoir modifié le nombre de nœuds dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="3ad59-211">Cette opération permet à la topologie d’ajuster le parallélisme pour compenser l’augmentation ou la diminution du nombre de nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="3ad59-212">Pour plus d’informations, consultez la rubrique <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Présentation du parallélisme d’une topologie Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="3ad59-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="3ad59-213">**Supprimer**: met fin à une topologie Storm après expiration du délai spécifié.</span><span class="sxs-lookup"><span data-stu-id="3ad59-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="3ad59-214">**Topology stats**: statistiques relatives à la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="3ad59-215">Utilisez les liens de la colonne **Fenêtre** pour définir l’intervalle de temps des entrées restantes sur la page.</span><span class="sxs-lookup"><span data-stu-id="3ad59-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="3ad59-216">**Spouts**: les spouts utilisés par la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="3ad59-217">Utilisez les liens de cette section pour afficher plus d’informations sur des spouts spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3ad59-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="3ad59-218">**Bolts**: les bolts utilisés par la topologie.</span><span class="sxs-lookup"><span data-stu-id="3ad59-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="3ad59-219">Utilisez les liens de cette section pour afficher plus d’informations sur des bolts spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3ad59-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="3ad59-220">**Configuration de la topologie**: configuration de la topologie sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="3ad59-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="3ad59-221">Résumé relatif aux spouts et aux bolts</span><span class="sxs-lookup"><span data-stu-id="3ad59-221">Spout and Bolt summary</span></span>

<span data-ttu-id="3ad59-222">La sélection d’un spout à partir de la section **Spouts** ou **Bolts** affiche les informations suivantes sur l’élément sélectionné :</span><span class="sxs-lookup"><span data-stu-id="3ad59-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="3ad59-223">**Résumé du composant**: des informations de base sur le spout ou le bolt.</span><span class="sxs-lookup"><span data-stu-id="3ad59-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="3ad59-224">**Statistiques du spout/bolt**: des statistiques relatives au spout ou au bolt.</span><span class="sxs-lookup"><span data-stu-id="3ad59-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="3ad59-225">Utilisez les liens de la colonne **Fenêtre** pour définir l’intervalle de temps des entrées restantes sur la page.</span><span class="sxs-lookup"><span data-stu-id="3ad59-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="3ad59-226">**Statistiques d’entrée** (bolt uniquement) : des informations sur les flux d’entrée consommés par le bolt.</span><span class="sxs-lookup"><span data-stu-id="3ad59-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="3ad59-227">**Statistiques de sortie**: des informations sur les flux de données émis par ce spout ou ce bolt.</span><span class="sxs-lookup"><span data-stu-id="3ad59-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="3ad59-228">**Exécuteurs**: informations sur les instances du spout ou du bolt.</span><span class="sxs-lookup"><span data-stu-id="3ad59-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="3ad59-229">Sélectionnez l’entrée **Port** d’un exécuteur spécifique afin d’afficher le journal des informations de diagnostic généré pour cette instance.</span><span class="sxs-lookup"><span data-stu-id="3ad59-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="3ad59-230">**Erreurs**: les informations d’erreur pour ce spout ou ce bolt.</span><span class="sxs-lookup"><span data-stu-id="3ad59-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="3ad59-231">Surveiller et gérer : API REST</span><span class="sxs-lookup"><span data-stu-id="3ad59-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="3ad59-232">L’interface utilisateur Storm repose sur l’API REST, ce qui vous permet de profiter de fonctionnalités de gestion et de surveillance similaires à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="3ad59-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="3ad59-233">À l'aide de l'API REST, vous pouvez créer des outils personnalisés pour gérer et surveiller les topologies Storm.</span><span class="sxs-lookup"><span data-stu-id="3ad59-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="3ad59-234">Pour plus d’informations, consultez la rubrique [API REST de l’interface utilisateur Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="3ad59-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="3ad59-235">Les informations suivantes sont spécifiques à l’utilisation de l’API REST avec Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ad59-236">L’API REST Storm n’est pas disponible publiquement sur Internet et est accessible à l’aide d’un tunnel SSH vers le nœud principal du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="3ad59-237">Pour plus d’informations sur la création et l’utilisation d’un tunnel SSH, consultez [Utilisation d’un tunnel SSH pour accéder à l’interface utilisateur web Ambari, ResourceManager, JobHistory, NameNode, Oozie et d’autres interfaces utilisateur web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="3ad59-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="3ad59-238">URI de base</span><span class="sxs-lookup"><span data-stu-id="3ad59-238">Base URI</span></span>

<span data-ttu-id="3ad59-239">L’URI de base pour l’API REST sur des clusters HDInsight sous Linux est disponible sur le nœud principal à l’adresse **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="3ad59-240">Le nom de domaine du nœud principal est généré lors de la création du cluster et n’est pas statique.</span><span class="sxs-lookup"><span data-stu-id="3ad59-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="3ad59-241">Vous trouverez le nom de domaine complet (FQDN) du nœud principal du cluster de plusieurs façons différentes :</span><span class="sxs-lookup"><span data-stu-id="3ad59-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="3ad59-242">**À partir d’une session SSH** : utilisez la commande `headnode -f` à partir d’une session SSH vers le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="3ad59-243">**À partir d’Ambari Web** : sélectionnez **Services** en haut de la page, puis sélectionnez **Storm**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="3ad59-244">Sous l’onglet **Résumé**, sélectionnez **Serveur de l’interface utilisateur de Storm**.</span><span class="sxs-lookup"><span data-stu-id="3ad59-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="3ad59-245">Le nom de domaine complet du nœud que l’interface utilisateur de Storm et l’API REST exécutent figure en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="3ad59-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="3ad59-246">**À partir de l’API REST d’Ambari** : utilisez la commande `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` pour extraire des informations sur le nœud sur lequel l’interface utilisateur de Storm et l’API REST s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="3ad59-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="3ad59-247">Remplacez **PASSWORD** par le mot de passe de l’administrateur du cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="3ad59-248">Remplacez **CLUSTERNAME** par le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="3ad59-249">Dans la réponse, l’entrée « host_name » contient le nom de domaine complet du nœud.</span><span class="sxs-lookup"><span data-stu-id="3ad59-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="3ad59-250">Authentification</span><span class="sxs-lookup"><span data-stu-id="3ad59-250">Authentication</span></span>

<span data-ttu-id="3ad59-251">Les requêtes à l’API REST doivent utiliser l’ **authentification de base**avec le nom et le mot de passe d’administrateur de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ad59-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad59-252">Étant donné que l’authentification de base est envoyée en texte clair, vous devez **toujours** utiliser HTTPS pour sécuriser les communications avec le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="3ad59-253">Valeurs de retour</span><span class="sxs-lookup"><span data-stu-id="3ad59-253">Return values</span></span>

<span data-ttu-id="3ad59-254">Les informations renvoyées par l’API REST sont uniquement utilisables au sein du cluster ou des machines virtuelles sur le même réseau virtuel Azure que le cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad59-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="3ad59-255">Par exemple, le nom de domaine complet (FQDN) retourné pour les serveurs Zookeeper n’est pas accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="3ad59-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ad59-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ad59-256">Next Steps</span></span>

<span data-ttu-id="3ad59-257">Maintenant que vous avez appris à déployer et surveiller des topologies à l’aide du tableau de bord Storm, découvrez comment [développer des topologies Java à l’aide de Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3ad59-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="3ad59-258">Pour accéder à une liste d’exemples supplémentaires de topologies, consultez la rubrique [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3ad59-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
