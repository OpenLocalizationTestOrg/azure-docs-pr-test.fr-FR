---
title: "Déploiement et gestion des topologies Apache Storm sur HDInsight | Microsoft Docs"
description: "Apprenez à déployer, surveiller et gérer des topologies Apache Storm à l’aide du tableau de bord Storm sur HDInsight. Utilisez les outils Hadoop pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="02918-104">Déploiement et gestion des topologies Apache Storm sur HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="02918-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="02918-105">Le tableau de bord Storm vous permet de déployer et d’exécuter des topologies Apache Storm sur votre cluster HDInsight à l’aide votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="02918-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="02918-106">Vous pouvez également utiliser le tableau de bord pour surveiller et gérer des topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="02918-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="02918-107">Si vous utilisez Visual Studio, les outils HDInsight pour Visual Studio fournissent des fonctionnalités similaires dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02918-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="02918-108">Le tableau de bord Storm et les fonctionnalités Storm des outils HDInsight s’appuient sur l’API REST Storm, qui peut être utilisée pour créer vos propres solutions d’analyse et de gestion.</span><span class="sxs-lookup"><span data-stu-id="02918-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02918-109">Les étapes décrites dans ce document nécessitent un tableau de bord Storm sur un cluster HDInsight utilisant Windows comme système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="02918-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="02918-110">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="02918-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="02918-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="02918-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="02918-112">Pour plus d’informations sur le déploiement et la gestion des topologies avec un cluster HDInsight utilisant Linux, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="02918-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02918-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="02918-113">Prerequisites</span></span>

* <span data-ttu-id="02918-114">**Apache Storm sur HDInsight** : pour connaître les étapes de création d’un cluster, voir [Prise en main d’Apache Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="02918-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="02918-115">Pour le **tableau de bord Storm**: un navigateur Web moderne qui prend en charge HTML5.</span><span class="sxs-lookup"><span data-stu-id="02918-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="02918-116">Pour **Visual Studio** : le Kit de développement logiciel (SDK) Azure 2.5.1 ou une version ultérieure et les outils HDInsight pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02918-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="02918-117">Consultez la rubrique [Prise en main de HDInsight Tools pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) pour installer et configurer les outils HDInsight pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02918-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="02918-118">L’une des versions suivantes de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="02918-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="02918-119">Visual Studio 2012 avec Update 4</span><span class="sxs-lookup"><span data-stu-id="02918-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="02918-120">Visual Studio 2013 avec Update 4 ou Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="02918-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="02918-121">Visual Studio 2015 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="02918-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="02918-122">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="02918-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="02918-123">Tableau de bord Storm</span><span class="sxs-lookup"><span data-stu-id="02918-123">Storm Dashboard</span></span>

<span data-ttu-id="02918-124">Le tableau de bord Storm est une page web disponible sur votre cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="02918-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="02918-125">L’URL est **https://&lt;clustername>.azurehdinsight.net/**, où **clustername** est le nom de votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02918-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="02918-126">Dans la partie supérieure du tableau de bord Storm, sélectionnez **Soumettre la topologie**.</span><span class="sxs-lookup"><span data-stu-id="02918-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="02918-127">Suivez les instructions affichées sur la page pour exécuter une topologie d’exemple ou pour télécharger et exécuter une topologie que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="02918-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![la page d’envoi de la topologie][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="02918-129">Interface utilisateur de Storm</span><span class="sxs-lookup"><span data-stu-id="02918-129">Storm UI</span></span>

<span data-ttu-id="02918-130">Dans le tableau de bord Storm, sélectionnez le lien **Interface utilisateur de Storm** .</span><span class="sxs-lookup"><span data-stu-id="02918-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="02918-131">Ce lien affiche les informations sur le cluster, ainsi que les topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="02918-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![l’interface utilisateur Storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="02918-133">Avec certaines versions d'Internet Explorer, vous constaterez peut-être que l'interface utilisateur Storm n'est pas actualisée après votre première visite.</span><span class="sxs-lookup"><span data-stu-id="02918-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="02918-134">Par exemple, elle n’affiche pas les nouvelles topologies que vous avez soumises, ou indique qu’une topologie est active alors que vous l’avez précédemment arrêtée.</span><span class="sxs-lookup"><span data-stu-id="02918-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="02918-135">Microsoft est conscient de ce problème et recherche actuellement une solution.</span><span class="sxs-lookup"><span data-stu-id="02918-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="02918-136">Page principale</span><span class="sxs-lookup"><span data-stu-id="02918-136">Main page</span></span>

<span data-ttu-id="02918-137">La page principale de l’interface utilisateur de Storm fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="02918-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="02918-138">**Résumé du cluster**: des informations de base sur le cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="02918-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="02918-139">**Résumé de la topologie**: une liste des topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="02918-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="02918-140">Utilisez les liens de cette section pour afficher plus d’informations sur les topologies spécifiques.</span><span class="sxs-lookup"><span data-stu-id="02918-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="02918-141">**Résumé du superviseur**: des informations sur le superviseur Storm.</span><span class="sxs-lookup"><span data-stu-id="02918-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="02918-142">**Configuration Nimbus**: configuration Nimbus du cluster.</span><span class="sxs-lookup"><span data-stu-id="02918-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="02918-143">Résumé de la topologie</span><span class="sxs-lookup"><span data-stu-id="02918-143">Topology summary</span></span>

<span data-ttu-id="02918-144">La sélection d’un lien de la section **Résumé de la topologie** affiche les informations suivantes sur la topologie :</span><span class="sxs-lookup"><span data-stu-id="02918-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="02918-145">**Résumé de la topologie**:des informations de base sur la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="02918-146">**Actions de la topologie**: les actions de gestion que vous pouvez effectuer sur la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="02918-147">**Activer**: reprend le traitement d’une topologie arrêtée.</span><span class="sxs-lookup"><span data-stu-id="02918-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="02918-148">**Désactiver**: suspend une topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="02918-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="02918-149">**Rééquilibrer**: ajuste le parallélisme de la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="02918-150">Il convient de rééquilibrer les topologies en cours d’exécution après avoir modifié le nombre de nœuds dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="02918-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="02918-151">Cela permet à la topologie d’ajuster le parallélisme pour compenser l’augmentation ou la diminution du nombre de nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="02918-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="02918-152">Pour plus d’informations, consultez [Présentation du parallélisme d’une topologie Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="02918-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="02918-153">**Supprimer**: met fin à une topologie Storm après expiration du délai spécifié.</span><span class="sxs-lookup"><span data-stu-id="02918-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="02918-154">**Topology stats**: statistiques relatives à la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="02918-155">Utilisez les liens de la colonne **Fenêtre** pour définir l’intervalle de temps des entrées restantes sur la page.</span><span class="sxs-lookup"><span data-stu-id="02918-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="02918-156">**Spouts**: les spouts utilisés par la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="02918-157">Utilisez les liens de cette section pour afficher plus d’informations sur des spouts spécifiques.</span><span class="sxs-lookup"><span data-stu-id="02918-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="02918-158">**Bolts**: les bolts utilisés par la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="02918-159">Utilisez les liens de cette section pour afficher plus d’informations sur des bolts spécifiques.</span><span class="sxs-lookup"><span data-stu-id="02918-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="02918-160">**Configuration de la topologie**: configuration de la topologie sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="02918-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="02918-161">Résumé relatif aux spouts et aux bolts</span><span class="sxs-lookup"><span data-stu-id="02918-161">Spout and Bolt summary</span></span>

<span data-ttu-id="02918-162">La sélection d’un spout à partir de la section **Spouts** ou **Bolts** affiche les informations suivantes sur l’élément sélectionné :</span><span class="sxs-lookup"><span data-stu-id="02918-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="02918-163">**Résumé du composant**: des informations de base sur le spout ou le bolt.</span><span class="sxs-lookup"><span data-stu-id="02918-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="02918-164">**Statistiques du spout/bolt**: des statistiques relatives au spout ou au bolt.</span><span class="sxs-lookup"><span data-stu-id="02918-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="02918-165">Utilisez les liens de la colonne **Fenêtre** pour définir l’intervalle de temps des entrées restantes sur la page.</span><span class="sxs-lookup"><span data-stu-id="02918-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="02918-166">**Statistiques d’entrée** (bolt uniquement) : des informations sur les flux d’entrée consommés par le bolt.</span><span class="sxs-lookup"><span data-stu-id="02918-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="02918-167">**Statistiques de sortie**: des informations sur les flux de données émis par ce spout ou ce bolt.</span><span class="sxs-lookup"><span data-stu-id="02918-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="02918-168">**Exécuteurs**: informations sur les instances du spout ou du bolt.</span><span class="sxs-lookup"><span data-stu-id="02918-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="02918-169">Sélectionnez l’entrée **Port** d’un exécuteur spécifique afin d’afficher le journal des informations de diagnostic généré pour cette instance.</span><span class="sxs-lookup"><span data-stu-id="02918-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="02918-170">**Erreurs**: les informations d’erreur pour ce spout ou ce bolt.</span><span class="sxs-lookup"><span data-stu-id="02918-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="02918-171">Outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02918-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="02918-172">Les outils HDInsight permettent de soumettre des topologies C# ou hybrides à votre cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="02918-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="02918-173">La procédure suivante utilise un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="02918-173">The following steps use a sample application.</span></span> <span data-ttu-id="02918-174">Pour plus d’informations sur la création de vos propres topologies à l’aide des outils HDInsight, consultez [Développement de topologies C# à l’aide des outils HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="02918-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="02918-175">Utilisez les étapes suivantes pour déployer un exemple sur votre Storm sur le cluster HDInsight, puis afficher et gérer la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="02918-176">Si vous n’avez pas encore installé la dernière version des outils HDInsight pour Visual Studio, consultez [Prise en main de HDInsight Tools pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="02918-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="02918-177">Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="02918-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="02918-178">Dans la boîte de dialogue **Nouveau projet**, développez **Installé** > **Modèles**, puis sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="02918-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="02918-179">Dans la liste des modèles, sélectionnez **Exemple Storm**.</span><span class="sxs-lookup"><span data-stu-id="02918-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="02918-180">En bas de la boîte de dialogue, entrez un nom pour l’application.</span><span class="sxs-lookup"><span data-stu-id="02918-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="02918-182">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet, puis sélectionnez **Envoyer à Storm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="02918-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02918-183">Si vous y êtes invité, entrez les informations d’identification de connexion pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="02918-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="02918-184">Si vous disposez de plusieurs abonnements, connectez-vous à celui qui contient votre cluster Storm dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02918-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="02918-185">Sélectionnez votre Storm sur le cluster HDInsight dans la liste déroulante **Cluster Storm**, puis sélectionnez **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="02918-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="02918-186">Vous pouvez contrôler si l’envoi a bien été effectué à l’aide de la fenêtre **Sortie** .</span><span class="sxs-lookup"><span data-stu-id="02918-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="02918-187">Lorsque la topologie a été envoyée avec succès, les **Topologies Storm** du cluster doivent apparaître.</span><span class="sxs-lookup"><span data-stu-id="02918-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="02918-188">Sélectionnez la topologie à partir de la liste pour afficher des informations sur la topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="02918-188">Select the topology from the list to view information about the running topology.</span></span>

    ![Visual Studio Monitor](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="02918-190">Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs** en développant **Azure** > **HDInsight**, puis en cliquant avec le bouton droit sur le cluster HDInsight et en sélectionnant **Affichage des topologies Storm**.</span><span class="sxs-lookup"><span data-stu-id="02918-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="02918-191">Sélectionnez la forme des spouts et bolts pour afficher des informations sur ces composants.</span><span class="sxs-lookup"><span data-stu-id="02918-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="02918-192">Une nouvelle fenêtre s’ouvre pour chaque élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="02918-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02918-193">Le nom de la topologie représente le nom de classe de la topologie (dans ce cas, `HelloWord`,) avec ajout d’un horodatage.</span><span class="sxs-lookup"><span data-stu-id="02918-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="02918-194">Dans la vue **Résumé de la topologie**, sélectionnez **Supprimer** pour arrêter la topologie.</span><span class="sxs-lookup"><span data-stu-id="02918-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02918-195">Les topologies Storm poursuivent leur exécution jusqu'à ce qu'elles soient arrêtées ou que le cluster soit supprimé.</span><span class="sxs-lookup"><span data-stu-id="02918-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="02918-196">API REST</span><span class="sxs-lookup"><span data-stu-id="02918-196">REST API</span></span>

<span data-ttu-id="02918-197">L’interface utilisateur Storm repose sur l’API REST, ce qui vous permet de profiter de fonctionnalités de gestion et de surveillance similaires à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="02918-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="02918-198">À l'aide de l'API REST, vous pouvez créer des outils personnalisés pour gérer et surveiller les topologies Storm.</span><span class="sxs-lookup"><span data-stu-id="02918-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="02918-199">Pour plus d’informations, consultez la rubrique [API REST de l’interface utilisateur Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="02918-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="02918-200">Les informations suivantes sont spécifiques à l’utilisation de l’API REST avec Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02918-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="02918-201">URI de base</span><span class="sxs-lookup"><span data-stu-id="02918-201">Base URI</span></span>

<span data-ttu-id="02918-202">L’URI de base pour l’API REST sur les clusters HDInsight est **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, où **clustername** est le nom de votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02918-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="02918-203">Authentification</span><span class="sxs-lookup"><span data-stu-id="02918-203">Authentication</span></span>

<span data-ttu-id="02918-204">Les requêtes à l’API REST doivent utiliser l’ **authentification de base**avec le nom et le mot de passe d’administrateur de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02918-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="02918-205">Étant donné que l’authentification de base est envoyée en texte clair, vous devez **toujours** utiliser HTTPS pour sécuriser les communications avec le cluster.</span><span class="sxs-lookup"><span data-stu-id="02918-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="02918-206">Valeurs de retour</span><span class="sxs-lookup"><span data-stu-id="02918-206">Return values</span></span>

<span data-ttu-id="02918-207">Les informations renvoyées par l’API REST sont uniquement utilisables au sein du cluster ou des machines virtuelles sur le même réseau virtuel Azure que le cluster.</span><span class="sxs-lookup"><span data-stu-id="02918-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="02918-208">Par exemple, le nom de domaine complet (FQDN) retourné pour les serveurs Zookeeper n’est pas accessible à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="02918-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02918-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02918-209">Next Steps</span></span>

<span data-ttu-id="02918-210">Maintenant que vous avez appris à déployer et surveiller des topologies à l’aide du tableau de bord Storm, découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="02918-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="02918-211">Développer des topologies C# à l’aide des outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02918-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="02918-212">Développer des topologies basées sur Java à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="02918-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="02918-213">Pour accéder à une liste d’exemples supplémentaires de topologies, consultez la rubrique [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="02918-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
