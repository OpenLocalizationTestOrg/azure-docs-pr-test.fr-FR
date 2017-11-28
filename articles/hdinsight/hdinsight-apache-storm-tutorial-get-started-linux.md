---
title: Exemples storm-starter sur Apache Storm sur HDInsight - Azure | Microsoft Docs
description: "Découvrez comment procéder à des analyses de Big Data et traiter les données en temps réel à l’aide d’Apache Storm et des exemples storm-starter sur HDInsight."
keywords: storm-starter, exemple apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 83fc6db1ddb43eb87e7c58684505d7196c1e53d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="bf79c-104">Prise en main d’Apache Storm sur HDInsight à l’aide des exemples storm-starter</span><span class="sxs-lookup"><span data-stu-id="bf79c-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="bf79c-105">Découvrez comment utiliser Apache Storm dans HDInsight à l’aide des exemples storm-starter.</span><span class="sxs-lookup"><span data-stu-id="bf79c-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="bf79c-106">Apache Storm est un système de calcul en temps réel, évolutif, distribué, à tolérance de panne, qui permet de traiter des flux de données.</span><span class="sxs-lookup"><span data-stu-id="bf79c-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="bf79c-107">Avec Storm sur Azure HDInsight, vous pouvez créer un cluster Storm basé sur le cloud qui effectue l’analyse de données volumineuses en temps réel.</span><span class="sxs-lookup"><span data-stu-id="bf79c-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf79c-108">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="bf79c-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bf79c-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bf79c-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf79c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf79c-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="bf79c-111">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="bf79c-111">**An Azure subscription**.</span></span> <span data-ttu-id="bf79c-112">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="bf79c-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="bf79c-113">**Des connaissances en SSH et SCP**.</span><span class="sxs-lookup"><span data-stu-id="bf79c-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="bf79c-114">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bf79c-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="bf79c-115">Créer un cluster Storm</span><span class="sxs-lookup"><span data-stu-id="bf79c-115">Create a Storm cluster</span></span>

<span data-ttu-id="bf79c-116">Utilisez les étapes suivantes pour créer un Storm sur un cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="bf79c-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="bf79c-117">À partir du [portail Azure](https://portal.azure.com), sélectionnez **+ et Nouveau**, **Intelligence et analyse**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bf79c-117">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Création d'un cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="bf79c-119">Dans le panneau **De base**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf79c-119">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="bf79c-120">**Nom du cluster** : nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf79c-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="bf79c-121">**Abonnement** : sélectionnez l'abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="bf79c-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="bf79c-122">**Nom d’utilisateur de connexion du cluster** et **Mot de passe de connexion du cluster** : les informations de connexion lors de l’accès au cluster sur HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf79c-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="bf79c-123">Vous utilisez ces informations d’identification pour accéder aux services tels que l’interface utilisateur Ambari Web ou l’API REST.</span><span class="sxs-lookup"><span data-stu-id="bf79c-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="bf79c-124">**Nom d’utilisateur Secure Shell (SSH)** : information de connexion utilisée lors de l’accès au cluster sur SSH.</span><span class="sxs-lookup"><span data-stu-id="bf79c-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="bf79c-125">Par défaut, le mot de passe est le même que le mot de passe de connexion de cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="bf79c-126">**Groupe de ressources** : groupe de ressources dans lequel créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="bf79c-127">**Emplacement** : la région Azure dans laquelle créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-127">**Location**: The Azure region to create the cluster in.</span></span>

    ![Sélectionnez un abonnement](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="bf79c-129">Sélectionnez le **Type de cluster**, puis définissez les valeurs suivantes sur le panneau **Configuration du cluster** :</span><span class="sxs-lookup"><span data-stu-id="bf79c-129">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="bf79c-130">**Type de cluster** : Storm</span><span class="sxs-lookup"><span data-stu-id="bf79c-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="bf79c-131">**Système d’exploitation** : Linux</span><span class="sxs-lookup"><span data-stu-id="bf79c-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="bf79c-132">**Version** : Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="bf79c-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="bf79c-133">**Niveau cluster** : standard</span><span class="sxs-lookup"><span data-stu-id="bf79c-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="bf79c-134">Enfin, utilisez le bouton **Sélectionner** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="bf79c-134">Finally, use the **Select** button to save settings.</span></span>

    ![Sélectionner un type de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="bf79c-136">Après avoir sélectionné le type de cluster, utilisez le bouton __Sélectionner__ pour définir le type de cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-136">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="bf79c-137">Ensuite, utilisez le bouton __Suivant__ bouton pour terminer la configuration de base.</span><span class="sxs-lookup"><span data-stu-id="bf79c-137">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="bf79c-138">À partir du panneau **Stockage**, sélectionnez ou créer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="bf79c-138">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="bf79c-139">Pour les étapes de ce document, laissez les autres champs de ce panneau sur leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="bf79c-139">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="bf79c-140">Utilisez le bouton __Suivant__ pour enregistrer la configuration de stockage.</span><span class="sxs-lookup"><span data-stu-id="bf79c-140">Use the __Next__ button to save storage configuration.</span></span>

    ![Définir les paramètres de compte de stockage pour HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="bf79c-142">Dans le panneau **Résumé**, passez en revue la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-142">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="bf79c-143">Utilisez les liens __Modifier__ pour modifier les éventuels paramètres incorrects.</span><span class="sxs-lookup"><span data-stu-id="bf79c-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="bf79c-144">Pour finir, cliquez sur le bouton __Créer__ pour créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-144">Finally, use the__Create__ button to create the cluster.</span></span>

    ![Résumé de la configuration du cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="bf79c-146">La création du cluster peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="bf79c-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="bf79c-147">Exécuter un exemple storm-starter sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="bf79c-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="bf79c-148">Connectez-vous au cluster HDInsight à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="bf79c-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="bf79c-149">Si vous utilisez un mot de passe pour sécuriser votre compte utilisateur SSH, vous serez invité à le saisir.</span><span class="sxs-lookup"><span data-stu-id="bf79c-149">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="bf79c-150">Si vous utilisez une clé publique, vous devrez peut-être utiliser le paramètre `-i` pour spécifier la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="bf79c-150">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="bf79c-151">Par exemple, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="bf79c-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="bf79c-152">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bf79c-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bf79c-153">Utilisez la commande suivante pour démarrer un exemple de topologie :</span><span class="sxs-lookup"><span data-stu-id="bf79c-153">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="bf79c-154">Sur les versions antérieures de HDInsight, le nom de classe de la topologie est `storm.starter.WordCountTopology` au lieu de `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="bf79c-154">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="bf79c-155">Cette commande démarre l’exemple de topologie WordCount sur le cluster, avec le nom convivial « wordcount ».</span><span class="sxs-lookup"><span data-stu-id="bf79c-155">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="bf79c-156">Elle génère des phrases de manière aléatoire et compte les occurrences de chaque mot dans ces phrases.</span><span class="sxs-lookup"><span data-stu-id="bf79c-156">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf79c-157">Pendant l’envoi de vos propres topologies au cluster, vous devez d’abord copier le fichier jar contenant le cluster avant d’utiliser la commande `storm`.</span><span class="sxs-lookup"><span data-stu-id="bf79c-157">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="bf79c-158">Utilisez la commande `scp` pour copier le fichier.</span><span class="sxs-lookup"><span data-stu-id="bf79c-158">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="bf79c-159">Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="bf79c-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="bf79c-160">L’exemple WordCount et d’autres exemples storm-starter sont déjà inclus dans votre cluster sous `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="bf79c-160">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="bf79c-161">Si vous êtes intéressé par la source des exemples storm-starter, vous trouverez le code à l’adresse [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="bf79c-161">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="bf79c-162">Ce lien concerne Storm 1.1.x, qui est fourni avec HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="bf79c-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="bf79c-163">Pour les autres versions de Storm, utilisez le bouton __Branche__ situé en haut de la page pour sélectionner une autre version de Storm.</span><span class="sxs-lookup"><span data-stu-id="bf79c-163">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="bf79c-164">Analyse de la topologie</span><span class="sxs-lookup"><span data-stu-id="bf79c-164">Monitor the topology</span></span>

<span data-ttu-id="bf79c-165">L’interface utilisateur Storm fournit une interface web incluse dans votre cluster HDInsight pour utiliser les topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf79c-165">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="bf79c-166">Suivez la procédure ci-après pour surveiller la topologie à l’aide de l’interface utilisateur de Storm.</span><span class="sxs-lookup"><span data-stu-id="bf79c-166">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="bf79c-167">Pour afficher l’interface utilisateur Storm, ouvrez un navigateur web et accédez à l’adresse https://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="bf79c-167">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="bf79c-168">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-168">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf79c-169">Si vous êtes invité à fournir un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster (admin) et le mot de passe que vous avez utilisé pour la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-169">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="bf79c-170">Sous **Résumé de la topologie**, sélectionnez l’entrée **Statistiques** située dans la colonne **Nom**.</span><span class="sxs-lookup"><span data-stu-id="bf79c-170">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="bf79c-171">Vous obtenez plus d’informations sur la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf79c-171">Information about the topology is displayed.</span></span>

    ![Tableau de bord Storm avec les informations sur la topologie WordCount storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="bf79c-173">Cette page fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf79c-173">This page provides the following information:</span></span>

    * <span data-ttu-id="bf79c-174">**Statistiques de topologie** : informations de base sur les performances de la topologie, organisées dans des fenêtres de temps.</span><span class="sxs-lookup"><span data-stu-id="bf79c-174">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="bf79c-175">La sélection d’une fenêtre de temps spécifique modifie la fenêtre de temps pour les informations affichées dans d’autres sections de la page.</span><span class="sxs-lookup"><span data-stu-id="bf79c-175">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="bf79c-176">**Spouts** : informations de base sur les spouts, y compris la dernière erreur retournée par chaque spout.</span><span class="sxs-lookup"><span data-stu-id="bf79c-176">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="bf79c-177">**Bolts** : informations de base sur les bolts.</span><span class="sxs-lookup"><span data-stu-id="bf79c-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="bf79c-178">**Configuration de la topologie** : informations détaillées sur la configuration de la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf79c-178">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="bf79c-179">Cette page présente également les actions qui peuvent être effectuées sur la topologie :</span><span class="sxs-lookup"><span data-stu-id="bf79c-179">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="bf79c-180">**Activer** : reprend le traitement d’une topologie désactivée.</span><span class="sxs-lookup"><span data-stu-id="bf79c-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="bf79c-181">**Désactiver** : suspend une topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf79c-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="bf79c-182">**Rééquilibrer** : ajuste le parallélisme de la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf79c-182">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="bf79c-183">Il convient de rééquilibrer les topologies en cours d’exécution après avoir modifié le nombre de nœuds dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-183">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="bf79c-184">Le rééquilibrage ajuste le parallélisme pour compenser l’augmentation/la réduction du nombre de nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="bf79c-184">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="bf79c-185">Pour plus d’informations, consultez la rubrique [Présentation du parallélisme d’une topologie Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="bf79c-185">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="bf79c-186">**Supprimer** : met fin à une topologie Storm après expiration du délai spécifié.</span><span class="sxs-lookup"><span data-stu-id="bf79c-186">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="bf79c-187">À partir de cette page, sélectionnez une entrée dans la section **Spouts** ou **Bolts**.</span><span class="sxs-lookup"><span data-stu-id="bf79c-187">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="bf79c-188">Vous obtenez des informations relatives au composant sélectionné.</span><span class="sxs-lookup"><span data-stu-id="bf79c-188">Information about the selected component is displayed.</span></span>

    ![Tableau de bord Storm avec des informations sur les composants sélectionnés.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="bf79c-190">Cette page affiche les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf79c-190">This page displays the following information:</span></span>

    * <span data-ttu-id="bf79c-191">**Statistiques du spout/bolt** : informations de base sur les performances de la topologie, organisées dans des fenêtres de temps.</span><span class="sxs-lookup"><span data-stu-id="bf79c-191">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="bf79c-192">La sélection d’une fenêtre de temps spécifique modifie la fenêtre de temps pour les informations affichées dans d’autres sections de la page.</span><span class="sxs-lookup"><span data-stu-id="bf79c-192">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="bf79c-193">**Statistiques d’entrée** (bolt uniquement) : informations sur les composants qui produisent des données consommées par le bolt.</span><span class="sxs-lookup"><span data-stu-id="bf79c-193">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="bf79c-194">**Statistiques de sortie** : informations sur les données émises par ce bolt.</span><span class="sxs-lookup"><span data-stu-id="bf79c-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="bf79c-195">**Exécuteurs** : informations sur les instances de ce composant.</span><span class="sxs-lookup"><span data-stu-id="bf79c-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="bf79c-196">**Erreurs** : erreurs générées par ce composant.</span><span class="sxs-lookup"><span data-stu-id="bf79c-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="bf79c-197">Lorsque vous affichez les détails d’un spout ou d’un bolt, sélectionnez une entrée depuis la colonne **Port** située dans la section **Exécuteurs** pour afficher les détails d’une instance spécifique du composant.</span><span class="sxs-lookup"><span data-stu-id="bf79c-197">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="bf79c-198">Dans cet exemple, le mot **sept** compte 1 493 957 occurrences.</span><span class="sxs-lookup"><span data-stu-id="bf79c-198">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="bf79c-199">C’est le nombre de fois où le mot a été détecté depuis le démarrage de cette topologie.</span><span class="sxs-lookup"><span data-stu-id="bf79c-199">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="bf79c-200">Arrêt de la topologie</span><span class="sxs-lookup"><span data-stu-id="bf79c-200">Stop the topology</span></span>

<span data-ttu-id="bf79c-201">Retournez à la page **Résumé de la topologie**, puis sélectionnez le bouton **Supprimer** de la section **Actions de topologie**.</span><span class="sxs-lookup"><span data-stu-id="bf79c-201">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="bf79c-202">Lorsque vous êtes invité à entrer le nombre de secondes à attendre avant l’arrêt de la topologie, entrez le nombre 10.</span><span class="sxs-lookup"><span data-stu-id="bf79c-202">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="bf79c-203">Après le délai d’expiration, la topologie n’apparaît plus quand vous vous rendez dans la section **Interface utilisateur Storm** du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="bf79c-203">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="bf79c-204">Suppression du cluster</span><span class="sxs-lookup"><span data-stu-id="bf79c-204">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="bf79c-205">Si vous rencontrez un problème lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="bf79c-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="bf79c-206"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf79c-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="bf79c-207">Dans ce didacticiel Apache Storm, vous avez découvert les principes de base de l’utilisation de Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf79c-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="bf79c-208">À présent, découvrez comment [développer des topologies basées sur Java à l’aide de Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bf79c-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="bf79c-209">Si vous êtes déjà familiarisé avec le développement de topologies basées sur Java et que vous souhaitez déployer une topologie existante dans HDInsight, consultez la page [Déploiement et gestion des topologies Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bf79c-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="bf79c-210">Si vous êtes un développeur .NET, vous pouvez créer des topologies C# ou C#/Java hybrides à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf79c-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="bf79c-211">Pour plus d’informations, consultez la rubrique [Développer des topologies C# pour Apache Storm sur HDInsight en utilisant les outils Hadoop pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bf79c-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="bf79c-212">Consultez les exemples suivants de topologies qui peuvent être utilisées avec Storm sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="bf79c-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="bf79c-213">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="bf79c-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
