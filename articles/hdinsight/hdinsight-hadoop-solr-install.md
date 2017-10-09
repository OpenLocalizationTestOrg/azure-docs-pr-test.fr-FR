---
title: "tooinstall d’Action de Script aaaUse Solr sur le cluster Hadoop - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight cluster avec Solr à l’aide d’Action de Script."
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
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="61512-103">Installer et utiliser Solr sur les clusters HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="61512-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="61512-104">Découvrez comment toocustomize HDInsight de basés sur Windows en cluster avec Solr à l’aide d’Action de Script et toouse Solr toosearch données.</span><span class="sxs-lookup"><span data-stu-id="61512-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61512-105">les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="61512-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="61512-106">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="61512-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="61512-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="61512-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="61512-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="61512-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="61512-109">Pour plus d’informations sur l’utilisation de Solr avec un cluster Linux, consultez [Installation et utilisation de Solr sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="61512-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="61512-110">Vous pouvez installer Solr sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*.</span><span class="sxs-lookup"><span data-stu-id="61512-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="61512-111">Un tooinstall de script d’exemple Solr sur un cluster HDInsight est disponible à partir d’un objet blob de stockage de Azure en lecture seule à [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="61512-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="61512-112">exemple de script Hello fonctionne uniquement avec la version 3.1 du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61512-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="61512-113">Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="61512-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="61512-114">exemple de script Hello utilisé dans cette rubrique crée un cluster basé sur Windows de Solr avec une configuration spécifique.</span><span class="sxs-lookup"><span data-stu-id="61512-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="61512-115">Si vous souhaitez que le cluster de Solr hello tooconfigure avec différents regroupements, partitions, schémas, les réplicas, etc., vous devez modifier le script de hello et les fichiers binaires de Solr en conséquence.</span><span class="sxs-lookup"><span data-stu-id="61512-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="61512-116">**Articles connexes**</span><span class="sxs-lookup"><span data-stu-id="61512-116">**Related articles**</span></span>

* [<span data-ttu-id="61512-117">Installer et utiliser Solr sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="61512-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="61512-118">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61512-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="61512-119">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="61512-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="61512-120">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="61512-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="61512-121">Présentation de Solr</span><span class="sxs-lookup"><span data-stu-id="61512-121">What is Solr?</span></span>
<span data-ttu-id="61512-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> est une plateforme de recherche d’entreprise qui permet d’effectuer de puissantes opérations de recherche en texte intégral sur des données.</span><span class="sxs-lookup"><span data-stu-id="61512-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="61512-123">Tandis que Hadoop permet de stocker et gérer des quantités importantes de données, Apache Solr fournit les fonctionnalités de recherche hello tooquickly extraire des données hello.</span><span class="sxs-lookup"><span data-stu-id="61512-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="61512-124">Installer Solr à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="61512-124">Install Solr using portal</span></span>
1. <span data-ttu-id="61512-125">Démarrer la création d’un cluster à l’aide de hello **création personnalisée** option, comme décrit dans [Hadoop de créer des clusters dans HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="61512-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="61512-126">Sur hello **Actions de Script** page de l’Assistant de hello, cliquez sur **ajouter une action de script** tooprovide des détails sur l’action de script hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="61512-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="61512-127">![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize d’Action de Script d’utiliser un cluster")</span><span class="sxs-lookup"><span data-stu-id="61512-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="61512-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="61512-128">Property</span></span></th><th><span data-ttu-id="61512-129">Valeur</span><span class="sxs-lookup"><span data-stu-id="61512-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="61512-130">Nom</span><span class="sxs-lookup"><span data-stu-id="61512-130">Name</span></span></td>
            <td><span data-ttu-id="61512-131">Spécifiez un nom pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="61512-131">Specify a name for hello script action.</span></span> <span data-ttu-id="61512-132">Par exemple, <b>Installation Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="61512-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="61512-133">URI du script</span><span class="sxs-lookup"><span data-stu-id="61512-133">Script URI</span></span></td>
            <td><span data-ttu-id="61512-134">Spécifier le script de toohello d’identificateur de ressource uniforme (URI) hello qui est appelée toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="61512-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="61512-135">Par exemple, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="61512-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="61512-136">Type de nœud</span><span class="sxs-lookup"><span data-stu-id="61512-136">Node Type</span></span></td>
            <td><span data-ttu-id="61512-137">Spécifiez les nœuds hello sur lequel le script de personnalisation hello est exécuté.</span><span class="sxs-lookup"><span data-stu-id="61512-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="61512-138">Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.</span><span class="sxs-lookup"><span data-stu-id="61512-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="61512-139">Paramètres</span><span class="sxs-lookup"><span data-stu-id="61512-139">Parameters</span></span></td>
            <td><span data-ttu-id="61512-140">Spécifiez des paramètres de hello, si requis par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="61512-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="61512-141">Hello script tooinstall Solr ne nécessite pas de paramètres, donc vous laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="61512-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="61512-142">Vous pouvez ajouter plusieurs tooinstall d’action de script de plusieurs composants sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="61512-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="61512-143">Après avoir ajouté les scripts hello, cliquez sur toostart de coche hello création hello cluster.</span><span class="sxs-lookup"><span data-stu-id="61512-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="61512-144">Utiliser Solr</span><span class="sxs-lookup"><span data-stu-id="61512-144">Use Solr</span></span>
<span data-ttu-id="61512-145">Vous devez commencer par indexer Solr avec quelques fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="61512-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="61512-146">Vous pouvez ensuite utiliser des requêtes de recherche toorun Solr sur les données de salutation indexée.</span><span class="sxs-lookup"><span data-stu-id="61512-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="61512-147">Effectuez hello suivant les étapes toouse Solr dans un cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="61512-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="61512-148">**Utilisez tooremote du protocole RDP (Remote Desktop) dans le cluster HDInsight de hello avec Solr installé**.</span><span class="sxs-lookup"><span data-stu-id="61512-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="61512-149">À partir de hello portail Azure, activer le Bureau à distance pour cluster hello que vous avez créé avec le cluster de hello installé et ensuite à distance dans Solr.</span><span class="sxs-lookup"><span data-stu-id="61512-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="61512-150">Pour obtenir des instructions, consultez [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="61512-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="61512-151">**Indexez Solr en téléchargeant des fichiers de données**.</span><span class="sxs-lookup"><span data-stu-id="61512-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="61512-152">Lorsque vous indexez Solr, vous placez les documents que vous devrez peut-être toosearch sur.</span><span class="sxs-lookup"><span data-stu-id="61512-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="61512-153">tooindex Solr, tooremote RDP d’utilisation dans un cluster de hello, accédez toohello bureau, ouvrez la ligne de commande Hadoop hello et accédez trop**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="61512-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="61512-154">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="61512-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="61512-155">Vous verrez hello suivant de sortie de console de hello :</span><span class="sxs-lookup"><span data-stu-id="61512-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="61512-156">utilitaire de post.jar Hello indexe Solr avec deux exemples de documents, **solr.xml** et **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="61512-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="61512-157">utilitaire de post.jar Hello et de documents hello sont disponibles avec l’installation de Solr.</span><span class="sxs-lookup"><span data-stu-id="61512-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="61512-158">**Utilisez hello Solr du tableau de bord toosearch dans hello les documents indexés**.</span><span class="sxs-lookup"><span data-stu-id="61512-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="61512-159">Dans toohello de session RDP hello HDInsight de cluster, ouvrez Internet Explorer et lancer le tableau de bord hello Solr à **http://headnodehost:8983/solr / #/**.</span><span class="sxs-lookup"><span data-stu-id="61512-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="61512-160">À partir du volet de gauche hello, à partir de hello **Core sélecteur** liste déroulante, sélectionnez **collection1**, dans ce cas, cliquez sur **requête**.</span><span class="sxs-lookup"><span data-stu-id="61512-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="61512-161">En tant qu’exemple, tooselect et retourner tous les documents hello dans Solr, fournissent hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="61512-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="61512-162">Bonjour **q** texte, entrez  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="61512-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="61512-163">Cela renvoie tous les documents de hello sont indexées de Solr.</span><span class="sxs-lookup"><span data-stu-id="61512-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="61512-164">Si vous souhaitez toosearch une chaîne spécifique au sein de documents de hello, vous pouvez entrer ici cette chaîne.</span><span class="sxs-lookup"><span data-stu-id="61512-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="61512-165">Bonjour **wt** zone de texte, le format de sortie hello select.</span><span class="sxs-lookup"><span data-stu-id="61512-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="61512-166">La valeur par défaut est **json**.</span><span class="sxs-lookup"><span data-stu-id="61512-166">Default is **json**.</span></span> <span data-ttu-id="61512-167">Cliquez sur **Exécuter la requête**.</span><span class="sxs-lookup"><span data-stu-id="61512-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="61512-168">![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "exécuter une requête sur un tableau de bord Solr")</span><span class="sxs-lookup"><span data-stu-id="61512-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="61512-169">sortie de Hello retourne hello deux documents que nous avons utilisés pour l’indexation de Solr.</span><span class="sxs-lookup"><span data-stu-id="61512-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="61512-170">sortie de Hello ressemble au suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="61512-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
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
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
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
4. <span data-ttu-id="61512-171">**Recommandé : Hello sauvegarder les données indexées de Solr tooAzure stockage d’objets Blob associé au cluster HDInsight de hello**.</span><span class="sxs-lookup"><span data-stu-id="61512-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="61512-172">Comme une bonne pratique, sauvegardez les données hello indexé à partir des nœuds de cluster hello Solr vers un stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="61512-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="61512-173">Effectuez hello suivant les étapes toodo ainsi :</span><span class="sxs-lookup"><span data-stu-id="61512-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="61512-174">À partir de la session RDP de hello, ouvrez Internet Explorer et toohello point suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="61512-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="61512-175">La réponse doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="61512-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="61512-176">Dans la session à distance de hello, accédez trop {SOLR_HOME}\{Collection} \data.</span><span class="sxs-lookup"><span data-stu-id="61512-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="61512-177">Pour cluster hello créé via un script d’exemple hello, cela doit être **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="61512-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="61512-178">À cet emplacement, vous devez voir un dossier de capture instantanée créé avec un nom similaire trop**instantané.* horodatage***.</span><span class="sxs-lookup"><span data-stu-id="61512-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="61512-179">Code postal du dossier de capture instantanée hello et téléchargez-le tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="61512-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="61512-180">À partir de la ligne de commande Hadoop hello, accédez à emplacement toohello du dossier de capture instantanée hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="61512-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="61512-181">Cette commande copie hello trop/exemple/captures instantanées/sous le conteneur hello au sein de la valeur par défaut de hello stockage compte associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="61512-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="61512-182">Installer Solr à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61512-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="61512-183">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="61512-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="61512-184">exemple Hello illustre comment tooinstall Spark à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61512-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="61512-185">Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="61512-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="61512-186">Installer Solr à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="61512-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="61512-187">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="61512-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="61512-188">exemple Hello illustre comment tooinstall Spark à l’aide de hello du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="61512-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="61512-189">Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="61512-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="61512-190">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="61512-190">See also</span></span>
* [<span data-ttu-id="61512-191">Installer et utiliser Solr sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="61512-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="61512-192">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61512-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="61512-193">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="61512-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="61512-194">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="61512-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="61512-195">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark.</span><span class="sxs-lookup"><span data-stu-id="61512-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="61512-196">[Installer R sur les clusters HDInsight][hdinsight-install-r] : exemple d’action de script sur l’installation de R.</span><span class="sxs-lookup"><span data-stu-id="61512-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="61512-197">[Installer Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemple d’action de script sur l’installation de Giraph.</span><span class="sxs-lookup"><span data-stu-id="61512-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
