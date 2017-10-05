---
title: "Kit de ressources Azure pour IntelliJ - Déboguer des applications à distance sur Spark HDInsight | Documents Microsoft"
description: "Découvrez comment utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ afin de déboguer à distance des applications exécutées sur des clusters Spark HDInsight via vpn."
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="ec45f-103">Utilisez le kit de ressources Azure pour IntelliJ pour déboguer des applications à distance sur HDInsight Spark via VPN</span><span class="sxs-lookup"><span data-stu-id="ec45f-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="ec45f-104">Nous vous recommandons le mode de débogage des applications spark à distance via ssh.</span><span class="sxs-lookup"><span data-stu-id="ec45f-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="ec45f-105">Pour obtenir des instructions, reportez-vous à la rubrique [Déboguer des applications Spark à distance sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="ec45f-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="ec45f-106">Cet article fournit des instructions pas à pas sur l’utilisation d’HDInsight Tools dans le kit de ressources Azure pour IntelliJ afin de soumettre un travail Spark sur un cluster Spark HDInsight et effectuer un débogage à distance à partir de votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="ec45f-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="ec45f-107">Pour ce faire, vous devez effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec45f-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="ec45f-108">Créer un réseau virtuel Azure de site à site ou de point à site.</span><span class="sxs-lookup"><span data-stu-id="ec45f-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="ec45f-109">Les étapes décrites dans ce document supposent d’utiliser un réseau de site à site.</span><span class="sxs-lookup"><span data-stu-id="ec45f-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="ec45f-110">Créer dans Azure HDInsight un cluster Spark faisant partie du réseau virtuel Azure de site à site.</span><span class="sxs-lookup"><span data-stu-id="ec45f-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="ec45f-111">Vérifier la connectivité entre votre ordinateur de bureau et le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="ec45f-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="ec45f-112">Créer une application Scala dans IntelliJ IDEA et la configurer pour le débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="ec45f-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="ec45f-113">Exécuter et déboguer l’application.</span><span class="sxs-lookup"><span data-stu-id="ec45f-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec45f-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ec45f-114">Prerequisites</span></span>
* <span data-ttu-id="ec45f-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ec45f-115">An Azure subscription.</span></span> <span data-ttu-id="ec45f-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ec45f-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="ec45f-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec45f-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ec45f-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ec45f-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="ec45f-119">Kit de développement logiciel (SDK) Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="ec45f-119">Oracle Java Development kit.</span></span> <span data-ttu-id="ec45f-120">Vous pouvez l’installer [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="ec45f-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="ec45f-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ec45f-121">IntelliJ IDEA.</span></span> <span data-ttu-id="ec45f-122">Cet article utilise la version 2017.1.</span><span class="sxs-lookup"><span data-stu-id="ec45f-122">This article uses version 2017.1.</span></span> <span data-ttu-id="ec45f-123">Vous pouvez l’installer à partir d’ [ici](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="ec45f-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="ec45f-124">HDInsight Tools dans le kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ec45f-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="ec45f-125">HDInsight Tools pour IntelliJ est disponible dans le cadre du kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ec45f-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="ec45f-126">Pour obtenir des instructions sur l’installation du kit de ressources Azure, voir [Installation du kit de ressources Azure pour IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="ec45f-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="ec45f-127">Connectez-vous à votre abonnement Azure à partir d’IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ec45f-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="ec45f-128">Suivez les instructions disponibles [ici](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="ec45f-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="ec45f-129">Lorsque vous exécutez l’application Spark Scala sur un ordinateur Windows pour un débogage à distance, vous pouvez obtenir une exception liée à l’absence d’un fichier WinUtils.exe sur Windows, comme expliqué dans le document [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) .</span><span class="sxs-lookup"><span data-stu-id="ec45f-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="ec45f-130">Pour résoudre cette erreur, vous devez [télécharger le fichier exécutable à partir d’ici](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) vers un emplacement tel que **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="ec45f-131">Vous devez ensuite ajouter une variable d’environnement **HADOOP_HOME** et définir la valeur de la variable sur **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="ec45f-132">Étape 1 : créer un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="ec45f-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="ec45f-133">Suivez les instructions contenues dans les liens ci-dessous pour créer un réseau virtuel Azure, puis vérifiez la connectivité entre votre ordinateur de bureau et le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="ec45f-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="ec45f-134">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec45f-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="ec45f-135">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec45f-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="ec45f-136">Configurer une connexion point à site à un réseau virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec45f-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="ec45f-137">Étape 2 : créer un cluster Spark HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="ec45f-138">Vous devez également créer dans Azure HDInsight un cluster Apache Spark faisant partie du réseau virtuel Azure que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="ec45f-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="ec45f-139">Utilisez les informations contenues dans l’article [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="ec45f-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="ec45f-140">Dans le cadre de la configuration facultative, sélectionnez le réseau virtuel Azure que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="ec45f-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="ec45f-141">Étape 3 : vérifier la connectivité entre votre ordinateur de bureau et le nœud principal du cluster</span><span class="sxs-lookup"><span data-stu-id="ec45f-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="ec45f-142">Récupérez l’adresse IP du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="ec45f-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="ec45f-143">Ouvrez l’interface utilisateur Ambari du cluster.</span><span class="sxs-lookup"><span data-stu-id="ec45f-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="ec45f-144">Dans le panneau du cluster, cliquez sur **Tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-144">From the cluster blade, click **Dashboard**.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="ec45f-146">À partir de l’interface utilisateur Ambari, cliquez sur **Hôtes**en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="ec45f-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="ec45f-148">Vous devez obtenir une liste de nœuds principaux, de nœuds worker et de nœuds zookeeper.</span><span class="sxs-lookup"><span data-stu-id="ec45f-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="ec45f-149">Les nœuds principaux sont repérés à l’aide du préfixe **hn***.</span><span class="sxs-lookup"><span data-stu-id="ec45f-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="ec45f-150">Cliquez sur le premier nœud principal.</span><span class="sxs-lookup"><span data-stu-id="ec45f-150">Click the first headnode.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="ec45f-152">En bas de la page qui s’ouvre, dans la zone **Résumé** , copiez l’adresse IP du nœud principal et le nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="ec45f-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="ec45f-154">Ajoutez l’adresse IP et le nom d’hôte du nœud principal au fichier **hosts** de l’ordinateur sur lequel vous souhaitez exécuter et déboguer à distance les travaux Spark.</span><span class="sxs-lookup"><span data-stu-id="ec45f-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="ec45f-155">Cela vous permettra de communiquer avec le nœud principal à l’aide de l’adresse IP et du nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="ec45f-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="ec45f-156">Ouvrez un bloc-notes avec des autorisations élevées.</span><span class="sxs-lookup"><span data-stu-id="ec45f-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="ec45f-157">Dans le menu Fichier, cliquez sur **Ouvrir** et accédez à l’emplacement du fichier hosts.</span><span class="sxs-lookup"><span data-stu-id="ec45f-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="ec45f-158">Sur un ordinateur Windows, ce fichier se trouve dans le répertoire `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="ec45f-159">Ajoutez le code suivant au fichier **hosts** .</span><span class="sxs-lookup"><span data-stu-id="ec45f-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="ec45f-160">À partir de l’ordinateur que vous avez connecté au réseau virtuel Azure utilisé par le cluster HDInsight, vérifiez que vous pouvez exécuter une commande ping sur les nœuds principaux aussi bien avec l’adresse IP qu’avec le nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="ec45f-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="ec45f-161">Exécutez une commande SSH dans le nœud principal du cluster en suivant les instructions fournies dans la section [Connexion à un cluster HDInsight sous Linux](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ec45f-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="ec45f-162">À partir du nœud principal du cluster, exécutez une commande ping sur l’adresse IP de l’ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="ec45f-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="ec45f-163">Vous devez tester la connectivité aux deux adresses IP affectées à l’ordinateur, une pour la connexion réseau et l’autre pour le réseau virtuel Azure auquel l’ordinateur est connecté.</span><span class="sxs-lookup"><span data-stu-id="ec45f-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="ec45f-164">Répétez également ces étapes pour l’autre nœud principal.</span><span class="sxs-lookup"><span data-stu-id="ec45f-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="ec45f-165">Étape 4 : créer une application Spark Scala à l’aide d’HDInsight Tools dans le kit de ressources Azure pour IntelliJ et la configurer pour le débogage à distance</span><span class="sxs-lookup"><span data-stu-id="ec45f-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="ec45f-166">Lancez IntelliJ IDEA et créez un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="ec45f-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="ec45f-167">Dans la boîte de dialogue Nouveau projet, choisissez les options suivantes, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![Créer une application Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="ec45f-169">Dans le volet gauche, sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="ec45f-170">Dans le volet droit, sélectionnez **Spark on HDInsight (Scala)**(Spark on HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="ec45f-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="ec45f-171">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-171">Click **Next**.</span></span>
2. <span data-ttu-id="ec45f-172">Dans la fenêtre suivante, fournissez les détails du projet suivants, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="ec45f-173">Fournissez un nom de projet et un emplacement de projet.</span><span class="sxs-lookup"><span data-stu-id="ec45f-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="ec45f-174">Pour **Projet SDK**, utilisez Java 1.8 pour le cluster Spark 2.x, Java 1.7 pour le cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="ec45f-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="ec45f-175">Pour la **version Spark**, l’assistant de création de projets Scala intègre la version correcte pour le kit de développement logiciel Spark et le kit de développement logiciel Scala.</span><span class="sxs-lookup"><span data-stu-id="ec45f-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="ec45f-176">Si la version du cluster Spark est inférieure à la version 2.0, choisissez Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="ec45f-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="ec45f-177">Dans le cas contraire, vous devez sélectionner spark2.x.</span><span class="sxs-lookup"><span data-stu-id="ec45f-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="ec45f-178">Cet exemple utilise Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="ec45f-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="ec45f-179">![Créer une application Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="ec45f-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="ec45f-180">Le projet Spark crée automatiquement un artefact à votre intention.</span><span class="sxs-lookup"><span data-stu-id="ec45f-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="ec45f-181">Pour voir l’artefact, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="ec45f-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="ec45f-182">Dans le menu **Fichier**, cliquez sur **Structure de projet**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="ec45f-183">Dans la boîte de dialogue **Structure de projet**, cliquez sur **Artefacts** pour afficher l’artefact créé par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec45f-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="ec45f-184">![Créer un fichier JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="ec45f-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="ec45f-185">Vous pouvez également créer votre propre artefact en cliquant sur l’icône **+** mis en surbrillance dans la capture d’écran ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ec45f-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="ec45f-186">Ajoutez des bibliothèques à votre projet.</span><span class="sxs-lookup"><span data-stu-id="ec45f-186">Add libraries to your project.</span></span> <span data-ttu-id="ec45f-187">Pour ajouter une bibliothèque, cliquez avec le bouton droit sur le nom du projet dans l’arborescence du projet, puis cliquez sur **Open Module Settings**(Ouvrir les paramètres du module).</span><span class="sxs-lookup"><span data-stu-id="ec45f-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="ec45f-188">Dans la boîte de dialogue **Structure de projet**, dans le volet gauche, cliquez sur **Bibliothèques**, cliquez sur le signe plus (+), puis cliquez sur **From Maven** (De Maven).</span><span class="sxs-lookup"><span data-stu-id="ec45f-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![Ajouter une bibliothèque](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="ec45f-190">Dans la boîte de dialogue **Download Library from Maven Repository** (Télécharger la bibliothèque à partir du référentiel Maven), recherchez et ajoutez les bibliothèques suivantes.</span><span class="sxs-lookup"><span data-stu-id="ec45f-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="ec45f-191">Copiez `yarn-site.xml` et `core-site.xml` à partir du nœud principal du cluster et ajoutez-les au projet.</span><span class="sxs-lookup"><span data-stu-id="ec45f-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="ec45f-192">Exécutez les commandes suivantes pour copier les fichiers.</span><span class="sxs-lookup"><span data-stu-id="ec45f-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="ec45f-193">Vous pouvez utiliser [Cygwin](https://cygwin.com/install.html) pour exécuter les commandes `scp` suivantes afin de copier les fichiers à partir des nœuds principaux du cluster.</span><span class="sxs-lookup"><span data-stu-id="ec45f-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="ec45f-194">Étant donné que nous avons déjà ajouté l’adresse IP et les noms d’hôtes des nœuds principaux du cluster au fichier hosts de notre ordinateur de bureau, nous pouvons utiliser les commandes **scp** de la manière suivante.</span><span class="sxs-lookup"><span data-stu-id="ec45f-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="ec45f-195">Ajoutez ces fichiers à votre projet en les copiant dans le dossier **/src** dans l’arborescence de votre projet, par exemple `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="ec45f-196">Mettez à jour le fichier `core-site.xml` pour effectuer les modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="ec45f-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="ec45f-197">`core-site.xml` inclut la clé chiffrée du compte de stockage associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="ec45f-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="ec45f-198">Dans le fichier `core-site.xml` que vous avez ajouté au projet, remplacez la clé chiffrée par la clé de stockage réelle associée au compte de stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec45f-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="ec45f-199">Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ec45f-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="ec45f-200">Supprimez les entrées suivantes du fichier `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-200">Remove the following entries from the `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="ec45f-201">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="ec45f-201">Save the file.</span></span>
7. <span data-ttu-id="ec45f-202">Ajoutez la classe principale pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ec45f-202">Add the Main class for your application.</span></span> <span data-ttu-id="ec45f-203">Dans l’**Explorateur de projets**, cliquez avec le bouton droit sur **src**, pointez sur **New** (Nouveau), puis cliquez sur **Scala class** (Classe Scala).</span><span class="sxs-lookup"><span data-stu-id="ec45f-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![Ajouter le code source](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="ec45f-205">Dans la boîte de dialogue **Create New Scala Class** (Créer une classe Scala), indiquez un nom, dans la zone **Kind** (Genre), sélectionnez **Object** (Objet), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Ajouter le code source](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="ec45f-207">Collez le code suivant dans le fichier `MyClusterAppMain.scala` .</span><span class="sxs-lookup"><span data-stu-id="ec45f-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="ec45f-208">Ce code crée le contexte Spark et lance une méthode `executeJob` à partir de l’objet `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

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

10. <span data-ttu-id="ec45f-209">Répétez les étapes 8 et 9 ci-dessus pour ajouter un nouvel objet Scala appelé `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="ec45f-210">Ajoutez le code suivant à cette classe.</span><span class="sxs-lookup"><span data-stu-id="ec45f-210">To this class add the following code.</span></span> <span data-ttu-id="ec45f-211">Ce code lit les données du fichier HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes qui contiennent uniquement un chiffre dans la septième colonne du fichier CSV et écrit la sortie dans **/HVACOut** sous le conteneur de stockage par défaut du cluster.</span><span class="sxs-lookup"><span data-stu-id="ec45f-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="ec45f-212">Répétez les étapes 8 et 9 ci-dessus pour ajouter une nouvelle classe appelée `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="ec45f-213">Cette classe implémente l’infrastructure de test Spark utilisée pour le débogage des applications.</span><span class="sxs-lookup"><span data-stu-id="ec45f-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="ec45f-214">Ajoutez le code suivant à la classe `RemoteClusterDebugging` .</span><span class="sxs-lookup"><span data-stu-id="ec45f-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="ec45f-215">Deux points importants sont ici à prendre en considération :</span><span class="sxs-lookup"><span data-stu-id="ec45f-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="ec45f-216">Pour `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, assurez-vous que le fichier JAR de l’assembly Spark est disponible sur le stockage de cluster dans le chemin d’accès spécifié.</span><span class="sxs-lookup"><span data-stu-id="ec45f-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="ec45f-217">Pour `setJars`, spécifiez l’emplacement où le fichier jar de l’artefact sera créé.</span><span class="sxs-lookup"><span data-stu-id="ec45f-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="ec45f-218">En général, il s’agit du répertoire `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="ec45f-219">Dans la classe `RemoteClusterDebugging`, cliquez avec le bouton droit sur le mot-clé `test` et sélectionnez **Create RemoteClusterDebugging Configuration** (Créer une configuration RemoteClusterDebugging).</span><span class="sxs-lookup"><span data-stu-id="ec45f-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="ec45f-221">Dans la boîte de dialogue, entrez un nom pour la configuration, puis sélectionnez **Test kind** (Type de test) comme **Test name** (Nom de test).</span><span class="sxs-lookup"><span data-stu-id="ec45f-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="ec45f-222">Laissez toutes les autres valeurs par défaut, cliquez sur **Appliquer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="ec45f-224">Une liste déroulante **Remote Run** (Exécution à distance) s’affiche maintenant dans la barre de menus.</span><span class="sxs-lookup"><span data-stu-id="ec45f-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="ec45f-226">Étape 5 : exécuter l’application en mode débogage</span><span class="sxs-lookup"><span data-stu-id="ec45f-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="ec45f-227">Dans votre projet IntelliJ IDEA, ouvrez `SparkSample.scala` et créez un point d’arrêt en regard de « val rdd1 ».</span><span class="sxs-lookup"><span data-stu-id="ec45f-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="ec45f-228">Dans le menu contextuel permettant de créer un point d’arrêt, sélectionnez **line in function executeJob**(ligne dans la fonction executeJob).</span><span class="sxs-lookup"><span data-stu-id="ec45f-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Ajouter un point d’arrêt](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="ec45f-230">Cliquez sur le bouton **Debug Run** (Exécuter le débogage) situé en regard de la liste déroulante de configuration **Remote Run** (Exécution à distance) pour commencer à exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="ec45f-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![Exécuter le programme en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="ec45f-232">Lorsque l’exécution du programme atteint le point d’arrêt, un onglet **Debugger** (Débogueur) doit apparaître dans le volet inférieur.</span><span class="sxs-lookup"><span data-stu-id="ec45f-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![Exécuter le programme en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="ec45f-234">Cliquez sur l’icône (**+**) pour ajouter une surveillance, comme l’illustre l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ec45f-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![Exécuter le programme en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="ec45f-236">Dans ce cas, étant donné que l’application s’est arrêtée avant la création de la variable `rdd1`, cette surveillance nous permet de voir les cinq premières lignes de la variable `rdd`.</span><span class="sxs-lookup"><span data-stu-id="ec45f-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="ec45f-237">Appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="ec45f-237">Press **ENTER**.</span></span>

    ![Exécuter le programme en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="ec45f-239">Dans l’image ci-dessus, on constate que, au moment de l’exécution, il est possible d’interroger des téraoctets de données et de corriger la progression de votre application.</span><span class="sxs-lookup"><span data-stu-id="ec45f-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="ec45f-240">Par exemple, dans la sortie illustrée ci-dessus, vous pouvez voir que la première ligne de la sortie est un en-tête.</span><span class="sxs-lookup"><span data-stu-id="ec45f-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="ec45f-241">Sur cette base, vous pouvez modifier votre code d’application pour ignorer la ligne d’en-tête si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ec45f-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="ec45f-242">Vous pouvez maintenant cliquer sur l’icône **Resume Program** (Reprendre le programme) pour poursuivre l’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="ec45f-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![Exécuter le programme en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="ec45f-244">Si l’application s’exécute correctement, vous devez obtenir une sortie similaire à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="ec45f-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![Exécuter le programme en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="ec45f-246"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ec45f-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ec45f-247">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="ec45f-248">Démonstration</span><span class="sxs-lookup"><span data-stu-id="ec45f-248">Demo</span></span>
* <span data-ttu-id="ec45f-249">Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="ec45f-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="ec45f-250">Débogage à distance (vidéo) : [Utiliser le kit de ressources Azure pour IntelliJ pour déboguer des applications Spark à distance sur un cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="ec45f-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="ec45f-251">Scénarios</span><span class="sxs-lookup"><span data-stu-id="ec45f-251">Scenarios</span></span>
* [<span data-ttu-id="ec45f-252">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="ec45f-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ec45f-253">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="ec45f-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ec45f-254">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="ec45f-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ec45f-255">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="ec45f-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ec45f-256">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ec45f-257">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="ec45f-257">Create and run applications</span></span>
* [<span data-ttu-id="ec45f-258">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="ec45f-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ec45f-259">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="ec45f-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ec45f-260">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="ec45f-260">Tools and extensions</span></span>
* [<span data-ttu-id="ec45f-261">Utiliser HDInsight Tools dans le kit de ressources Azure pour IntelliJ pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="ec45f-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ec45f-262">Utiliser le kit de ressources Azure pour IntelliJ pour déboguer des applications Spark à distance via SSH</span><span class="sxs-lookup"><span data-stu-id="ec45f-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="ec45f-263">Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="ec45f-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="ec45f-264">Utiliser HDInsight Tools dans le kit de ressources Azure pour Eclipse pour créer des applications Spark</span><span class="sxs-lookup"><span data-stu-id="ec45f-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="ec45f-265">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ec45f-266">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ec45f-267">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="ec45f-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ec45f-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster (Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight)</span><span class="sxs-lookup"><span data-stu-id="ec45f-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ec45f-269">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="ec45f-269">Manage resources</span></span>
* [<span data-ttu-id="ec45f-270">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ec45f-271">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec45f-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
