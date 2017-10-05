---
title: Utiliser une action de script pour installer Solr sur un cluster Hadoop - Azure | Documents Microsoft
description: "Découvrez comment personnaliser un cluster HDInsight avec Solr à l’aide d’une action de script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="70def-103">Installer et utiliser Solr sur les clusters HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="70def-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="70def-104">Découvrez comment personnaliser un cluster HDInsight basé sur Windows avec Solr à l’aide d’une action de script, et comment utiliser Solr pour explorer des données.</span><span class="sxs-lookup"><span data-stu-id="70def-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70def-105">Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="70def-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="70def-106">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="70def-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="70def-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="70def-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="70def-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="70def-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="70def-109">Pour plus d’informations sur l’utilisation de Solr avec un cluster Linux, consultez [Installation et utilisation de Solr sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="70def-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="70def-110">Vous pouvez installer Solr sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*.</span><span class="sxs-lookup"><span data-stu-id="70def-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="70def-111">Pour obtenir un exemple de script pour installer Solr sur un cluster HDInsight, téléchargez l’objet blob de stockage Azure en lecture seule à l’adresse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="70def-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="70def-112">L'exemple de script fonctionne uniquement avec un cluster HDInsight version 3.1.</span><span class="sxs-lookup"><span data-stu-id="70def-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="70def-113">Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="70def-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="70def-114">L’exemple de script utilisé dans cette rubrique crée un cluster Solr Windows avec une configuration spécifique.</span><span class="sxs-lookup"><span data-stu-id="70def-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="70def-115">Si vous souhaitez configurer le cluster Solr avec d'autres collections, partitions, schémas, réplicas, etc., vous devez modifier le script et les fichiers binaires Solr en conséquence.</span><span class="sxs-lookup"><span data-stu-id="70def-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="70def-116">**Articles connexes**</span><span class="sxs-lookup"><span data-stu-id="70def-116">**Related articles**</span></span>

* [<span data-ttu-id="70def-117">Installer et utiliser Solr sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="70def-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="70def-118">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70def-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="70def-119">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="70def-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="70def-120">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="70def-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="70def-121">Présentation de Solr</span><span class="sxs-lookup"><span data-stu-id="70def-121">What is Solr?</span></span>
<span data-ttu-id="70def-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> est une plateforme de recherche d’entreprise qui permet d’effectuer de puissantes opérations de recherche en texte intégral sur des données.</span><span class="sxs-lookup"><span data-stu-id="70def-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="70def-123">Alors que Hadoop permet de stocker et de gérer de grandes quantités de données, Apache Solr fournit les fonctionnalités de recherche nécessaires pour les récupérer rapidement.</span><span class="sxs-lookup"><span data-stu-id="70def-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="70def-124">Installer Solr à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="70def-124">Install Solr using portal</span></span>
1. <span data-ttu-id="70def-125">Démarrez la création d’un cluster à l’aide de l’option **CRÉATION PERSONNALISÉE** , comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="70def-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="70def-126">Sur la page **Actions de script** de l’Assistant, cliquez sur **ajouter l’action de script** pour fournir des informations sur l’action de script, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="70def-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="70def-127">![Utiliser Action de script pour personnaliser un cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Utiliser Action de script pour personnaliser un cluster")</span><span class="sxs-lookup"><span data-stu-id="70def-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="70def-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="70def-128">Property</span></span></th><th><span data-ttu-id="70def-129">Valeur</span><span class="sxs-lookup"><span data-stu-id="70def-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="70def-130">Nom</span><span class="sxs-lookup"><span data-stu-id="70def-130">Name</span></span></td>
            <td><span data-ttu-id="70def-131">Indiquez un nom pour l'action de script.</span><span class="sxs-lookup"><span data-stu-id="70def-131">Specify a name for the script action.</span></span> <span data-ttu-id="70def-132">Par exemple, <b>Installation Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="70def-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="70def-133">URI du script</span><span class="sxs-lookup"><span data-stu-id="70def-133">Script URI</span></span></td>
            <td><span data-ttu-id="70def-134">Spécifiez l'URI (Uniform Resource Identifier) du script appelé pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="70def-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="70def-135">Par exemple, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="70def-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="70def-136">Type de nœud</span><span class="sxs-lookup"><span data-stu-id="70def-136">Node Type</span></span></td>
            <td><span data-ttu-id="70def-137">Spécifiez les nœuds sur lesquels le script de personnalisation est exécuté.</span><span class="sxs-lookup"><span data-stu-id="70def-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="70def-138">Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.</span><span class="sxs-lookup"><span data-stu-id="70def-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="70def-139">parameters</span><span class="sxs-lookup"><span data-stu-id="70def-139">Parameters</span></span></td>
            <td><span data-ttu-id="70def-140">Spécifiez les paramètres, si le script le demande.</span><span class="sxs-lookup"><span data-stu-id="70def-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="70def-141">Le script d’installation de Solr ne nécessite aucun paramètre. Vous pouvez donc laisser ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="70def-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="70def-142">Vous pouvez ajouter plusieurs actions de script pour installer plusieurs composants sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="70def-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="70def-143">Après avoir ajouté les scripts, cliquez sur la coche pour démarrer la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="70def-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="70def-144">Utiliser Solr</span><span class="sxs-lookup"><span data-stu-id="70def-144">Use Solr</span></span>
<span data-ttu-id="70def-145">Vous devez commencer par indexer Solr avec quelques fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="70def-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="70def-146">Vous pouvez ensuite utiliser Solr pour exécuter des requêtes de recherche sur les données indexées.</span><span class="sxs-lookup"><span data-stu-id="70def-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="70def-147">Procédez comme suit pour utiliser Solr dans un cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="70def-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="70def-148">**Utilisez le protocole RDP (Remote Desktop) pour vous connecter à distance au cluster HDInsight avec Solr installé**.</span><span class="sxs-lookup"><span data-stu-id="70def-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="70def-149">À partir du portail Azure, activez le Bureau à distance pour le cluster que vous avez créé avec Solr installé, puis accédez à distance au cluster.</span><span class="sxs-lookup"><span data-stu-id="70def-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="70def-150">Pour la marche à suivre, consultez [Connexion à des clusters HDInsight à l’aide de RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="70def-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="70def-151">**Indexez Solr en téléchargeant des fichiers de données**.</span><span class="sxs-lookup"><span data-stu-id="70def-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="70def-152">Lorsque vous indexez Solr, vous y placez des documents sur lesquels vous devrez peut-être effectuer des recherches.</span><span class="sxs-lookup"><span data-stu-id="70def-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="70def-153">Pour indexer Solr, utilisez le protocole RDP pour vous connecter à distance au cluster, accédez au Bureau, ouvrez la ligne de commande Hadoop et accédez à **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="70def-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="70def-154">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70def-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="70def-155">Le résultat suivant s’affiche sur la console :</span><span class="sxs-lookup"><span data-stu-id="70def-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="70def-156">L’utilitaire post.jar indexe Solr avec deux exemples de documents : **solr.xml** et **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="70def-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="70def-157">L'utilitaire post.jar et les exemples de documents sont disponibles avec l'installation Solr.</span><span class="sxs-lookup"><span data-stu-id="70def-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="70def-158">**Utilisez le tableau de bord Solr pour effectuer une recherche dans les documents indexés**.</span><span class="sxs-lookup"><span data-stu-id="70def-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="70def-159">Dans la session RDP au cluster HDInsight, ouvrez Internet Explorer, puis lancez le tableau de bord Solr à l'adresse **http://headnodehost:8983/solr/#/**.</span><span class="sxs-lookup"><span data-stu-id="70def-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="70def-160">Dans la liste déroulante **Sélecteur de base** située dans le volet gauche, sélectionnez **collection1** et cliquez ensuite sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="70def-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="70def-161">Par exemple, pour sélectionner et renvoyer tous les documents dans Solr, renseignez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="70def-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="70def-162">Dans la zone de texte **q**, entrez **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="70def-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="70def-163">Tous les documents indexés dans Solr sont alors renvoyés.</span><span class="sxs-lookup"><span data-stu-id="70def-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="70def-164">Si vous souhaitez rechercher une chaîne spécifique dans les documents, vous pouvez la saisir à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="70def-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="70def-165">Sélectionnez le format de sortie dans la zone de texte **wt** .</span><span class="sxs-lookup"><span data-stu-id="70def-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="70def-166">La valeur par défaut est **json**.</span><span class="sxs-lookup"><span data-stu-id="70def-166">Default is **json**.</span></span> <span data-ttu-id="70def-167">Cliquez sur **Exécuter la requête**.</span><span class="sxs-lookup"><span data-stu-id="70def-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="70def-168">![Utiliser Action de Script pour personnaliser un cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Exécuter une requête sur un tableau de bord Solr")</span><span class="sxs-lookup"><span data-stu-id="70def-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="70def-169">La sortie renvoie les deux documents que nous avions utilisés pour indexer Solr.</span><span class="sxs-lookup"><span data-stu-id="70def-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="70def-170">La sortie se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="70def-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="70def-171">**Recommandé : sauvegardez les données indexées à partir de Solr dans un objet WASB (Azure Storage Blob) associé au cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="70def-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="70def-172">Il est conseillé de sauvegarder les données indexées à partir de nœuds de cluster Solr sur un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="70def-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="70def-173">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70def-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="70def-174">À partir de la session RDP, ouvrez Internet Explorer et accédez à l'URL suivante :</span><span class="sxs-lookup"><span data-stu-id="70def-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="70def-175">La réponse doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="70def-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="70def-176">Dans la session à distance, accédez à {SOLR_HOME}\{Collection}\data.</span><span class="sxs-lookup"><span data-stu-id="70def-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="70def-177">Pour le cluster créé à l’aide de l’exemple de script, il doit s’agir de **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="70def-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="70def-178">Un dossier d’instantanés créé avec un nom semblable à **snapshot.*timestamp*** doit normalement figurer à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="70def-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="70def-179">Compressez le dossier d’instantanés et téléchargez-le vers le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="70def-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="70def-180">À partir de la ligne de commande Hadoop, accédez à l’emplacement du dossier d’instantanés à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70def-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="70def-181">Cette commande copie l’instantané dans /example/data/ sous le conteneur, dans le compte de stockage par défaut associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="70def-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="70def-182">Installer Solr à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="70def-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="70def-183">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="70def-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="70def-184">L’exemple montre comment installer Spark avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70def-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="70def-185">Vous devez personnaliser le script pour utiliser [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="70def-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="70def-186">Installer Solr à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="70def-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="70def-187">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="70def-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="70def-188">L’exemple montre comment installer Spark à l’aide du Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="70def-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="70def-189">Vous devez personnaliser le script pour utiliser [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="70def-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="70def-190">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="70def-190">See also</span></span>
* [<span data-ttu-id="70def-191">Installer et utiliser Solr sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="70def-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="70def-192">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70def-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="70def-193">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="70def-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="70def-194">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="70def-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="70def-195">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark.</span><span class="sxs-lookup"><span data-stu-id="70def-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="70def-196">[Installer R sur les clusters HDInsight][hdinsight-install-r] : exemple d’action de script sur l’installation de R.</span><span class="sxs-lookup"><span data-stu-id="70def-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="70def-197">[Installer Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemple d’action de script sur l’installation de Giraph.</span><span class="sxs-lookup"><span data-stu-id="70def-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
