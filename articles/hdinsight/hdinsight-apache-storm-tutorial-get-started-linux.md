---
title: "exemples d’aaaStorm-starter sur Apache Storm sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment analytique de données volumineuses toodo et traiter les données en temps réel à l’aide d’Apache Storm hello exemples storm-starter sur HDInsight."
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
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="2cb4f-104">Prise en main Apache Storm sur HDInsight à l’aide des exemples de storm-starter hello</span><span class="sxs-lookup"><span data-stu-id="2cb4f-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="2cb4f-105">Découvrez comment toouse Apache Storm dans HDInsight à l’aide de hello exemples de storm-starter.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="2cb4f-106">Apache Storm est un système de calcul en temps réel, évolutif, distribué, à tolérance de panne, qui permet de traiter des flux de données.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="2cb4f-107">Avec Storm sur Azure HDInsight, vous pouvez créer un cluster Storm basé sur le cloud qui effectue l’analyse de données volumineuses en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cb4f-108">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2cb4f-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cb4f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2cb4f-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="2cb4f-111">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-111">**An Azure subscription**.</span></span> <span data-ttu-id="2cb4f-112">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="2cb4f-113">**Des connaissances en SSH et SCP**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="2cb4f-114">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="2cb4f-115">Créer un cluster Storm</span><span class="sxs-lookup"><span data-stu-id="2cb4f-115">Create a Storm cluster</span></span>

<span data-ttu-id="2cb4f-116">Utilisez hello suivant les étapes toocreate une tempête de cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="2cb4f-117">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez **+ nouveau**, **Intelligence + Analytique**, puis sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Création d'un cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="2cb4f-119">À partir de hello **notions de base** panneau, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="2cb4f-120">**Nom du cluster**: nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="2cb4f-121">**Abonnement**: sélectionnez hello abonnement toouse.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="2cb4f-122">**Nom d’utilisateur de cluster** et **mot de passe de connexion Cluster**: connexion hello lors de l’accès de cluster de hello via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="2cb4f-123">Vous utilisez ces services de tooaccess des informations d’identification telles que hello l’interface utilisateur de Ambari Web ou l’API REST.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="2cb4f-124">**Secure Shell (SSH) username**: connexion hello utilisée lors de l’accès de cluster de hello via SSH.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="2cb4f-125">Par défaut, un mot de passe hello est hello identique au mot de passe de connexion hello cluster.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="2cb4f-126">**Groupe de ressources**: hello ressource groupe toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="2cb4f-127">**Emplacement**: hello région Azure toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Sélectionnez un abonnement](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="2cb4f-129">Sélectionnez **Cluster type**, et puis hello du jeu de valeurs suivantes sur hello **configuration de Cluster** panneau :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="2cb4f-130">**Type de cluster** : Storm</span><span class="sxs-lookup"><span data-stu-id="2cb4f-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="2cb4f-131">**Système d’exploitation** : Linux</span><span class="sxs-lookup"><span data-stu-id="2cb4f-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="2cb4f-132">**Version** : Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="2cb4f-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="2cb4f-133">**Niveau cluster** : standard</span><span class="sxs-lookup"><span data-stu-id="2cb4f-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="2cb4f-134">Enfin, utilisez hello **sélectionnez** bouton toosave paramètres.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Sélectionner un type de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="2cb4f-136">Après avoir sélectionné le type de cluster hello, utilisez hello __sélectionnez__ tooset hello cluster type de bouton.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="2cb4f-137">Ensuite, utilisez hello __suivant__ configuration de base de toofinish de bouton.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="2cb4f-138">À partir de hello **stockage** panneau, sélectionnez ou créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="2cb4f-139">Pour connaître les étapes hello dans ce document, laissez hello autres champs sur ce panneau valeurs par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="2cb4f-140">Hello d’utilisation __suivant__ configuration du stockage toosave bouton.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Définir les paramètres de compte de stockage hello pour HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="2cb4f-142">À partir de hello **Résumé** panneau, revoir la configuration de cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="2cb4f-143">Hello d’utilisation __modifier__ lie toochange tous les paramètres sont incorrects.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="2cb4f-144">Enfin, utilisez le cluster de hello toocreate the__Create__ bouton.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Résumé de la configuration du cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="2cb4f-146">Il peut prendre jusqu'à cluster de hello toocreate too20 minutes.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="2cb4f-147">Exécuter un exemple storm-starter sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2cb4f-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="2cb4f-148">Connecter le cluster HDInsight de toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="2cb4f-149">Si vous avez utilisé un toosecure de mot de passe de votre compte d’utilisateur SSH, vous êtes invité à tooenter il.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="2cb4f-150">Si vous avez utilisé une clé publique, vous pouvez peut-être utiliser hello `-i` paramètre toospecify hello la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="2cb4f-151">Par exemple, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="2cb4f-152">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2cb4f-153">Utilisez hello suivant commande toostart un exemple de topologie :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="2cb4f-154">Dans les versions précédentes de HDInsight, nom de la classe hello de topologie de hello est `storm.starter.WordCountTopology` au lieu de `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="2cb4f-155">Cette commande démarre hello exemple WordCount de topologie sur cluster hello, avec un nom convivial 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="2cb4f-156">Il génère de manière aléatoire les phrases et les occurrences de hello de nombre de chaque mot dans les phrases hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2cb4f-157">Lorsque vous soumettez votre propre cluster toohello de topologies, vous devez d’abord copier le fichier jar hello contenant le cluster de hello avant d’utiliser hello `storm` commande.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="2cb4f-158">Hello d’utilisation `scp` fichier de commandes toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="2cb4f-159">Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="2cb4f-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="2cb4f-160">exemple WordCount de Hello et des autres exemples storm-starter, figurent déjà sur votre cluster à `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="2cb4f-161">Si vous êtes intéressé par source hello pour obtenir des exemples hello storm-starter, vous pouvez trouver le code hello au [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="2cb4f-162">Ce lien concerne Storm 1.1.x, qui est fourni avec HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="2cb4f-163">Pour les autres versions de Storm, utilisez hello __branche__ bouton haut hello hello page tooselect une autre version de Storm.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="2cb4f-164">Moniteur hello topologie</span><span class="sxs-lookup"><span data-stu-id="2cb4f-164">Monitor hello topology</span></span>

<span data-ttu-id="2cb4f-165">Bonjour Storm UI fournit une interface web pour l’utilisation des topologies en cours d’exécution et est inclus dans votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="2cb4f-166">Utilisez hello suivant la topologie de hello toomonitor étapes à l’aide de hello Storm UI :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="2cb4f-167">toodisplay hello Storm UI, ouvrez un web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="2cb4f-168">Remplacez **CLUSTERNAME** avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2cb4f-169">Si vous êtes invité tooprovide un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster hello (admin) et un mot de passe que vous avez utilisé lors des cluster hello création.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="2cb4f-170">Sous **récapitulatif de la topologie**, sélectionnez hello **wordcount** entrée Bonjour **nom** colonne.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="2cb4f-171">Informations sur la topologie hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-171">Information about hello topology is displayed.</span></span>

    ![Tableau de bord Storm avec les informations sur la topologie WordCount storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="2cb4f-173">Cette page fournit hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="2cb4f-174">**Statistiques de topologie** -informations de base sur les performances de topologie hello, organisés dans des fenêtres de temps.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="2cb4f-175">Sélection d’une fenêtre de temps de temps spécifique fenêtre modifications hello pour les informations affichées dans d’autres sections de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="2cb4f-176">**Becs verseurs amovibles** -informations de base sur becs verseurs, y compris hello dernière erreur retournée par chaque bec.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="2cb4f-177">**Bolts** : informations de base sur les bolts.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="2cb4f-178">**Configuration de la topologie** -des informations détaillées sur la configuration de la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="2cb4f-179">Cette page fournit également des actions qui peuvent être effectuées sur la topologie de hello :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="2cb4f-180">**Activer** : reprend le traitement d’une topologie désactivée.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="2cb4f-181">**Désactiver** : suspend une topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="2cb4f-182">**Rééquilibrer** -ajuste le parallélisme hello de topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="2cb4f-183">Vous devez rééquilibrer les topologies en cours d’exécution une fois que vous avez modifié le nombre de hello de nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="2cb4f-184">Rééquilibrage ajuste toocompensate de parallélisme pour le numéro d’augmenté/diminué hello de nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="2cb4f-185">Pour plus d’informations, consultez [présentation parallélisme hello d’une topologie de Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="2cb4f-186">**KILL** -met fin à une topologie Storm après hello spécifié le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="2cb4f-187">À partir de cette page, sélectionnez une entrée de hello **becs verseurs amovibles** ou **boulons** section.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="2cb4f-188">Pour plus d’informations à propos du composant sélectionné hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-188">Information about hello selected component is displayed.</span></span>

    ![Tableau de bord Storm avec des informations sur les composants sélectionnés.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="2cb4f-190">Cette page affiche hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="2cb4f-191">**BEC/éclair statistiques** -informations de base sur les performances du composant hello, organisés dans des fenêtres de temps.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="2cb4f-192">Sélection d’une fenêtre de temps de temps spécifique fenêtre modifications hello pour les informations affichées dans d’autres sections de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="2cb4f-193">**D’entrée statistiques** (boulon uniquement) - informations sur les composants qui produisent des données consommées par un éclair de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="2cb4f-194">**Statistiques de sortie** : informations sur les données émises par ce bolt.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="2cb4f-195">**Exécuteurs** : informations sur les instances de ce composant.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="2cb4f-196">**Erreurs** : erreurs générées par ce composant.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="2cb4f-197">Lorsque vous affichez les détails de hello d’un bec ou d’éclair, sélectionnez une entrée hello **Port** colonne Bonjour **exécuteurs** section tooview les détails d’une instance spécifique du composant de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="2cb4f-198">Dans cet exemple, hello word **sept** s’est produite 1493957 fois.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="2cb4f-199">Ce nombre est le nombre de fois hello a été rencontrée depuis le démarrage de cette topologie.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="2cb4f-200">Arrêter la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="2cb4f-200">Stop hello topology</span></span>

<span data-ttu-id="2cb4f-201">Retourner toohello **récapitulatif de la topologie** page topologie du nombre de mots hello et sélectionnez hello **Kill** bouton hello **actions de topologie** section.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="2cb4f-202">Lorsque vous y êtes invité, entrez 10 hello secondes toowait avant d’arrêter la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="2cb4f-203">Après le délai d’attente hello, topologie de hello n’apparaît plus lorsque vous visitez hello **Storm UI** section du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="2cb4f-204">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="2cb4f-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="2cb4f-205">Si vous rencontrez un problème lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="2cb4f-206"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2cb4f-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="2cb4f-207">Dans ce didacticiel d’Apache Storm, vous avez appris didacticiel hello utilisation Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="2cb4f-208">Ensuite, découvrez comment trop[basée sur Java de développer des topologies, à l’aide de Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="2cb4f-209">Si vous êtes déjà familiarisé avec le développement basé sur Java de topologies et que vous souhaitez toodeploy un tooHDInsight de topologie existante, consultez [déployer et gérer les topologies d’Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="2cb4f-210">Si vous êtes un développeur .NET, vous pouvez créer des topologies C# ou C#/Java hybrides à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2cb4f-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="2cb4f-211">Pour plus d’informations, consultez la rubrique [Développer des topologies C# pour Apache Storm sur HDInsight en utilisant les outils Hadoop pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2cb4f-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="2cb4f-212">Par exemple, les topologies qui peuvent être utilisés avec Storm sur HDInsight, consultez hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2cb4f-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="2cb4f-213">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2cb4f-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
