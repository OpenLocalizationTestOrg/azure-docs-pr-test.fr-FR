---
title: "aaaAzure boîte à outils pour IntelliJ - débogage des applications à distance sur HDInsight Spark | Documents Microsoft"
description: "Découvrez comment utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de débogage tooremotely IntelliJ en cours d’exécution sur des clusters HDInsight Spark via vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="3a3d3-103">Utilisez la boîte à outils Azure pour les applications de toodebug IntelliJ à distance sur HDInsight Spark via VPN</span><span class="sxs-lookup"><span data-stu-id="3a3d3-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="3a3d3-104">Nous vous recommandons de façon hello du débogage applicaltion spark à distance via ssh.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="3a3d3-105">Pour obtenir des instructions, reportez-vous à la rubrique [Déboguer des applications Spark à distance sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="3a3d3-106">Cet article fournit des instructions sur le toouse hello outils HDInsight dans la boîte à outils Azure pour IntelliJ toosubmit un travail Spark sur le cluster HDInsight Spark et déboguer à distance à partir de votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="3a3d3-107">toodo par conséquent, vous devez effectuer hello suivant les étapes principales :</span><span class="sxs-lookup"><span data-stu-id="3a3d3-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="3a3d3-108">Créer un réseau virtuel Azure de site à site ou de point à site.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="3a3d3-109">étapes de Hello dans ce document supposent que vous utilisez un réseau de site à site.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="3a3d3-110">Créez un cluster Spark dans Azure HDInsight qui fait partie de hello de site à site réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="3a3d3-111">Vérifiez la connectivité hello entre le nœud principal du cluster hello et votre bureau.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="3a3d3-112">Créer une application Scala dans IntelliJ IDEA et la configurer pour le débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="3a3d3-113">Exécuter et déboguer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a3d3-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3a3d3-114">Prerequisites</span></span>
* <span data-ttu-id="3a3d3-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-115">An Azure subscription.</span></span> <span data-ttu-id="3a3d3-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="3a3d3-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3a3d3-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="3a3d3-119">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-119">Oracle Java Development kit.</span></span> <span data-ttu-id="3a3d3-120">Vous pouvez l’installer [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="3a3d3-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-121">IntelliJ IDEA.</span></span> <span data-ttu-id="3a3d3-122">Cet article utilise la version 2017.1.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-122">This article uses version 2017.1.</span></span> <span data-ttu-id="3a3d3-123">Vous pouvez l’installer à partir d’ [ici](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="3a3d3-124">HDInsight Tools dans le kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="3a3d3-125">Outils HDInsight pour IntelliJ sont disponibles dans le cadre de la boîte à outils Azure pour IntelliJ de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="3a3d3-126">Pour obtenir des instructions sur la façon dont tooinstall hello boîte à outils Azure, consultez [installation Bonjour Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="3a3d3-127">Connectez-vous à votre abonnement Azure à partir d’IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="3a3d3-128">Suivez les instructions de hello [ici](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="3a3d3-129">Lorsque vous exécutez l’application Spark Scala pour le débogage distant sur un ordinateur Windows, vous pouvez obtenir une exception comme expliqué dans [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) qui se produit en raison de tooa manquant WinUtils.exe sur Windows.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="3a3d3-130">toowork autour de cette erreur, vous devez [télécharger hello exécutable à partir d’ici](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa emplacement comme **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="3a3d3-131">Vous devez ensuite ajouter une variable d’environnement **HADOOP_HOME** et la valeur hello de variable de hello trop**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="3a3d3-132">Étape 1 : créer un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="3a3d3-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="3a3d3-133">Suivez les instructions de hello hello ci-dessous des liens toocreate un réseau virtuel Azure, puis vérifiez la connectivité hello entre bureau de hello et réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="3a3d3-134">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3a3d3-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="3a3d3-135">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a3d3-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="3a3d3-136">Configurer un réseau virtuel de tooa de connexion de point à site à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a3d3-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="3a3d3-137">Étape 2 : créer un cluster Spark HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="3a3d3-138">Vous devez également créer un cluster d’Apache Spark sur Azure HDInsight qui fait partie de hello réseau virtuel Azure que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="3a3d3-139">Utilisez les informations hello disponibles à l’adresse [basés sur Linux de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="3a3d3-140">Dans le cadre de la configuration facultative, sélectionnez hello réseau virtuel Azure que vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="3a3d3-141">Étape 3 : Vérifier la connectivité de hello entre le nœud principal du cluster hello et votre bureau</span><span class="sxs-lookup"><span data-stu-id="3a3d3-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="3a3d3-142">Obtenir l’adresse IP de hello de nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="3a3d3-143">Ouvrez Ambari UI de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="3a3d3-144">Dans le panneau de cluster hello, cliquez sur **tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="3a3d3-146">À partir de hello Ambari UI, hello en haut à droite, cliquez sur **hôtes**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="3a3d3-148">Vous devez obtenir une liste de nœuds principaux, de nœuds worker et de nœuds zookeeper.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="3a3d3-149">Hello headnodes ont hello **hn*** préfixe.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="3a3d3-150">Cliquez sur le nœud principal de la première de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-150">Click hello first headnode.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="3a3d3-152">En bas de hello de page hello qui s’ouvre, à partir de hello **Résumé** zone, copie hello adresse IP de nœud principal de hello et nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="3a3d3-154">Inclure l’adresse hello et nom d’hôte hello de hello nœud principal toohello **hôtes** fichier sur l’ordinateur où vous voulez toorun, puis déboguez à distance les travaux de Spark hello hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="3a3d3-155">Cela vous permettra toocommunicate avec un nœud principal de hello à l’aide d’adresse IP de hello, ainsi que des nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="3a3d3-156">Ouvrez un bloc-notes avec des autorisations élevées.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="3a3d3-157">Dans le menu fichier de hello, cliquez sur **ouvrir** puis accédez emplacement toohello du fichier d’hôtes hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="3a3d3-158">Sur un ordinateur Windows, ce fichier se trouve dans le répertoire `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="3a3d3-159">Ajouter hello suivant toohello **hôtes** fichier.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="3a3d3-160">À partir de l’ordinateur hello que vous avez connecté toohello réseau virtuel Azure qui est utilisé par le cluster HDInsight de hello, vérifiez que vous pouvez tester les deux headnodes hello à l’aide d’adresse IP de hello, ainsi que des nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="3a3d3-161">SSH dans à l’aide d’instructions hello au nœud principal de cluster hello [cluster de HDInsight tooan de se connecter à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="3a3d3-162">À partir du nœud principal de cluster hello, ping l’adresse IP de hello d’ordinateur de bureau hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="3a3d3-163">Vous devez tester la connectivité tooboth hello attribués d’adresses IP toohello ordinateur, une pour la connexion de réseau hello et hello autre pour hello réseau virtuel Azure hello ordinateur est connecté à.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="3a3d3-164">Répétez les étapes de hello pour hello autre nœud principal également.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="3a3d3-165">Étape 4 : Créer une application Spark Scala à l’aide des outils de HDInsight hello dans la boîte à outils Azure pour IntelliJ et configurez-le pour le débogage distant</span><span class="sxs-lookup"><span data-stu-id="3a3d3-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="3a3d3-166">Lancez IntelliJ IDEA et créez un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="3a3d3-167">Dans la boîte de dialogue Nouveau projet hello, rendre hello des options suivantes, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Créer une application Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="3a3d3-169">Dans le volet gauche de hello, sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="3a3d3-170">Dans le volet droit de hello, sélectionnez **Spark sur HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="3a3d3-171">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-171">Click **Next**.</span></span>
2. <span data-ttu-id="3a3d3-172">Dans la fenêtre suivante de hello, fournir hello suivant des détails du projet, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="3a3d3-173">Fournissez un nom de projet et un emplacement de projet.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="3a3d3-174">Pour **Projet SDK**, utilisez Java 1.8 pour le cluster Spark 2.x, Java 1.7 pour le cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="3a3d3-175">Pour la **version Spark**, l’assistant de création de projets Scala intègre la version correcte pour le kit de développement logiciel Spark et le kit de développement logiciel Scala.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="3a3d3-176">Si la version du cluster spark hello est 2.0 inférieur, choisissez nouvelles 1.x.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="3a3d3-177">Dans le cas contraire, vous devez sélectionner spark2.x.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="3a3d3-178">Cet exemple utilise Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="3a3d3-179">![Créer une application Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="3a3d3-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="3a3d3-180">projet de Spark Hello créera automatiquement un artefact pour vous.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="3a3d3-181">artefact de hello toosee, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="3a3d3-182">À partir de hello **fichier** menu, cliquez sur **Structure de projet**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="3a3d3-183">Bonjour **Structure de projet** boîte de dialogue, cliquez sur **artefacts** toosee hello par défaut artefact qui est créé.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="3a3d3-184">![Créer un fichier JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="3a3d3-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="3a3d3-185">Vous pouvez également créer vos propres artefact Fix en cliquant sur hello  **+**  icône, mis en surbrillance dans l’image hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="3a3d3-186">Ajoutez les bibliothèques tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-186">Add libraries tooyour project.</span></span> <span data-ttu-id="3a3d3-187">tooadd une bibliothèque, cliquez sur le nom de projet hello dans l’arborescence du projet hello, puis cliquez sur **ouvrir les paramètres du Module**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="3a3d3-188">Bonjour **Structure de projet** boîte de dialogue, dans le volet gauche de hello, cliquez sur **bibliothèques**, cliquez sur le symbole de hello (+), puis cliquez sur **à partir de Maven**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Ajouter une bibliothèque](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="3a3d3-190">Bonjour **télécharger la bibliothèque à partir de Maven référentiel** boîte de dialogue zone, rechercher et ajouter hello suivant des bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="3a3d3-191">Copie `yarn-site.xml` et `core-site.xml` de hello nœud principal de cluster et l’ajouter toohello projet.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="3a3d3-192">Utilisez hello commandes toocopy hello fichiers suivants.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="3a3d3-193">Vous pouvez utiliser [Cygwin](https://cygwin.com/install.html) suivant de hello toorun `scp` fichiers hello toocopy hello cluster headnodes de commandes.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="3a3d3-194">Étant donné que nous avons ajouté déjà hello cluster nœud principal IP adresse et les noms d’hôtes fo hello fichier hosts sur le bureau de hello, nous pouvons utiliser hello **scp** commandes Bonjour suivant manière.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="3a3d3-195">Ajouter le projet tooyour de ces fichiers en les copiant sous hello **/src** dossier dans l’arborescence de votre projet, par exemple `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="3a3d3-196">Hello de mise à jour `core-site.xml` hello toomake modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="3a3d3-197">`core-site.xml`inclut le compte de stockage de clés toohello hello chiffré associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="3a3d3-198">Bonjour `core-site.xml` que vous avez ajouté le projet toohello, remplacer hello de clé chiffrée avec la clé de stockage réel hello associée au compte de stockage par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="3a3d3-199">Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="3a3d3-200">Supprimer hello suivant entrées hello `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="3a3d3-201">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-201">Save hello file.</span></span>
7. <span data-ttu-id="3a3d3-202">Ajoutez la classe de principal de hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-202">Add hello Main class for your application.</span></span> <span data-ttu-id="3a3d3-203">À partir de hello **Explorateur de projets**, avec le bouton droit **src**, pointez trop**nouveau**, puis cliquez sur **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Ajouter le code source](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="3a3d3-205">Bonjour **créer une nouvelle classe Scala** boîte de dialogue zone, fournissez un nom pour **type** sélectionnez **objet**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Ajouter le code source](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="3a3d3-207">Bonjour `MyClusterAppMain.scala` file, collez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="3a3d3-208">Ce code crée le contexte de Spark hello et lance un `executeJob` méthode hello `SparkSample` objet.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="3a3d3-209">Répétez les étapes 8 et 9 ci-dessus tooadd un nouvel objet Scala appelé `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="3a3d3-210">toothis classe ajouter hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-210">toothis class add hello following code.</span></span> <span data-ttu-id="3a3d3-211">Ce code lit les données de salutation hello HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes hello qui ont uniquement un chiffre dans la colonne septième hello hello CSV et écrit la sortie de hello trop**/HVACOut** sous la valeur par défaut de hello conteneur de stockage pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="3a3d3-212">Répétez les étapes 8 et 9 ci-dessus tooadd une nouvelle classe appelée `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="3a3d3-213">Cette classe implémente l’infrastructure de test de Spark hello est utilisé pour déboguer des applications.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="3a3d3-214">Ajouter hello suivant code toohello `RemoteClusterDebugging` classe.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="3a3d3-215">Deux toonote choses ici :</span><span class="sxs-lookup"><span data-stu-id="3a3d3-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="3a3d3-216">Pour `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, assurez-vous que hello l’assembly Spark JAR est disponible sur le stockage de cluster hello au chemin d’accès spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="3a3d3-217">Pour `setJars`, spécifier l’emplacement de hello où jar d’artefact hello sera créé.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="3a3d3-218">En général, il s’agit du répertoire `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="3a3d3-219">Bonjour `RemoteClusterDebugging` de classe, avec le bouton droit hello `test` (mot clé) et sélectionnez **créer une Configuration de RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="3a3d3-221">Dans la boîte de dialogue hello, fournissez un nom pour la configuration de hello et sélectionnez hello **Test type** en tant que **nom du Test**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="3a3d3-222">Laissez toutes les autres valeurs par défaut, cliquez sur **Appliquer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="3a3d3-224">Vous devez maintenant voir un **exécuter à distance** configuration liste déroulante dans la barre de menus hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="3a3d3-226">Étape 5 : Exécuter l’application hello en mode débogage</span><span class="sxs-lookup"><span data-stu-id="3a3d3-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="3a3d3-227">Dans votre projet IntelliJ idée, ouvrez `SparkSample.scala` et créer un rdd1 too'val suivant de point d’arrêt ».</span><span class="sxs-lookup"><span data-stu-id="3a3d3-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="3a3d3-228">Dans le menu contextuel de hello pour la création d’un point d’arrêt, sélectionnez **ligne dans la fonction executeJob**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Ajouter un point d’arrêt](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="3a3d3-230">Cliquez sur hello **déboguer exécuter** toohello suivant du bouton **exécuter à distance** toostart de liste déroulante de configuration application hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="3a3d3-232">Lorsque l’exécution du programme hello atteint un point d’arrêt hello, vous devez voir un **débogueur** onglet dans le volet du bas hello.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="3a3d3-234">Cliquez sur hello (**+**) icône tooadd un espion, comme indiqué dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="3a3d3-236">Ici, car l’application hello s’est arrêtée avant la variable de hello `rdd1` a été créé, à l’aide de cette espion que nous pouvons voir ce que sont hello 5 premières lignes dans la variable de hello `rdd`.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="3a3d3-237">Appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-237">Press **ENTER**.</span></span>

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="3a3d3-239">Ce que vous voyez dans l’image hello ci-dessus est que vous pouvez interroger terrabytes de données et de débogage lors de l’exécution, la progression de votre application.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="3a3d3-240">Par exemple, dans la sortie hello illustrée hello ci-dessus, vous pouvez voir que hello première ligne de sortie de hello est un en-tête.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="3a3d3-241">En fonction de cela, vous pouvez modifier la ligne d’en-tête hello tooskip application code si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="3a3d3-242">Vous pouvez maintenant cliquer sur hello **Resume programme** tooproceed icône avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="3a3d3-244">Si l’application hello se termine correctement, vous devez voir une sortie semblable à hello suivante.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="3a3d3-246"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3a3d3-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3a3d3-247">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="3a3d3-248">Démonstration</span><span class="sxs-lookup"><span data-stu-id="3a3d3-248">Demo</span></span>
* <span data-ttu-id="3a3d3-249">Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3a3d3-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="3a3d3-250">Débogage distant (vidéo) : [utilisation Azure Toolkit pour les applications de Spark IntelliJ toodebug à distance sur un HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3a3d3-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="3a3d3-251">Scénarios</span><span class="sxs-lookup"><span data-stu-id="3a3d3-251">Scenarios</span></span>
* [<span data-ttu-id="3a3d3-252">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="3a3d3-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3a3d3-253">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="3a3d3-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3a3d3-254">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3a3d3-255">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="3a3d3-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3a3d3-256">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3a3d3-257">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="3a3d3-257">Create and run applications</span></span>
* [<span data-ttu-id="3a3d3-258">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="3a3d3-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3a3d3-259">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="3a3d3-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3a3d3-260">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="3a3d3-260">Tools and extensions</span></span>
* [<span data-ttu-id="3a3d3-261">Utilisez les outils HDInsight dans la boîte à outils Azure pour IntelliJ toocreate et soumettre des applications les plus importantes Spark Scala</span><span class="sxs-lookup"><span data-stu-id="3a3d3-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3a3d3-262">Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via SSH</span><span class="sxs-lookup"><span data-stu-id="3a3d3-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="3a3d3-263">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="3a3d3-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="3a3d3-264">Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse</span><span class="sxs-lookup"><span data-stu-id="3a3d3-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="3a3d3-265">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3a3d3-266">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3a3d3-267">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="3a3d3-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3a3d3-268">Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="3a3d3-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3a3d3-269">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="3a3d3-269">Manage resources</span></span>
* [<span data-ttu-id="3a3d3-270">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a3d3-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3a3d3-271">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3a3d3-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
