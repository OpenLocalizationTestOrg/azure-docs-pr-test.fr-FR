---
title: "aaaInstall et l’utilisation des clusters Giraph sur Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight de cluster avec Giraph et toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="1c069-103">Installer et utiliser Giraph sur les clusters HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="1c069-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="1c069-104">Découvrez comment toocustomize Windows basé sur le cluster HDInsight porte Giraph utilisant l’Action de Script et graphiques de toouse Giraph tooprocess à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="1c069-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="1c069-105">Pour plus d’informations sur l’utilisation de Giraph avec un cluster Linux, consultez [Installation de Giraph sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c069-106">les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="1c069-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1c069-107">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="1c069-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1c069-108">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="1c069-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1c069-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1c069-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1c069-110">Pour plus d’informations sur la façon de tooinstall Giraph sur un cluster HDInsight de basés sur Linux, consultez [Giraph d’installer sur les clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="1c069-111">Vous pouvez installer Giraph sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*.</span><span class="sxs-lookup"><span data-stu-id="1c069-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="1c069-112">Un tooinstall de script d’exemple Giraph sur un cluster HDInsight est disponible à partir d’un objet blob de stockage de Azure en lecture seule à [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1c069-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="1c069-113">exemple de script Hello fonctionne uniquement avec la version 3.1 du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c069-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="1c069-114">Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="1c069-115">**Articles connexes**</span><span class="sxs-lookup"><span data-stu-id="1c069-115">**Related articles**</span></span>

* [<span data-ttu-id="1c069-116">Installer Giraph sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="1c069-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="1c069-117">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c069-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="1c069-118">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="1c069-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="1c069-119">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="1c069-120">Présentation de Giraph</span><span class="sxs-lookup"><span data-stu-id="1c069-120">What is Giraph?</span></span>
<span data-ttu-id="1c069-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c069-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="1c069-122">Graphiques de modéliser des relations entre les objets, tels que les connexions hello entre des routeurs d’un réseau de grande taille comme hello Internet, ou des relations entre des utilisateurs sur les réseaux sociaux (parfois désignée tooas un graphique social).</span><span class="sxs-lookup"><span data-stu-id="1c069-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="1c069-123">Le traitement du graphique vous permet de tooreason sur les relations hello entre les objets dans un graphique, telles que :</span><span class="sxs-lookup"><span data-stu-id="1c069-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="1c069-124">identifier les amis potentiels en fonction de vos relations actuelles ;</span><span class="sxs-lookup"><span data-stu-id="1c069-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="1c069-125">Identification hello la plus courte entre deux ordinateurs dans un réseau.</span><span class="sxs-lookup"><span data-stu-id="1c069-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="1c069-126">Calcul de rang dans la page hello des pages Web.</span><span class="sxs-lookup"><span data-stu-id="1c069-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="1c069-127">Installation de Giraph à l'aide du portail</span><span class="sxs-lookup"><span data-stu-id="1c069-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="1c069-128">Démarrer la création d’un cluster à l’aide de hello **création personnalisée** option, comme décrit dans [Hadoop de créer des clusters dans HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="1c069-129">Sur hello **Actions de Script** page de l’Assistant de hello, cliquez sur **ajouter une action de script** tooprovide des détails sur l’action de script hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c069-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="1c069-130">![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize d’Action de Script d’utiliser un cluster")</span><span class="sxs-lookup"><span data-stu-id="1c069-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="1c069-131">Propriété</span><span class="sxs-lookup"><span data-stu-id="1c069-131">Property</span></span></th><th><span data-ttu-id="1c069-132">Valeur</span><span class="sxs-lookup"><span data-stu-id="1c069-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="1c069-133">Nom</span><span class="sxs-lookup"><span data-stu-id="1c069-133">Name</span></span></td>
            <td><span data-ttu-id="1c069-134">Spécifiez un nom pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="1c069-134">Specify a name for hello script action.</span></span> <span data-ttu-id="1c069-135">Par exemple, <b>Installation Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="1c069-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="1c069-136">URI du script</span><span class="sxs-lookup"><span data-stu-id="1c069-136">Script URI</span></span></td>
            <td><span data-ttu-id="1c069-137">Spécifier le script de toohello d’identificateur de ressource uniforme (URI) hello qui est appelée toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="1c069-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="1c069-138">Par exemple, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="1c069-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="1c069-139">Type de nœud</span><span class="sxs-lookup"><span data-stu-id="1c069-139">Node Type</span></span></td>
            <td><span data-ttu-id="1c069-140">Spécifiez les nœuds hello sur lequel le script de personnalisation hello est exécuté.</span><span class="sxs-lookup"><span data-stu-id="1c069-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="1c069-141">Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.</span><span class="sxs-lookup"><span data-stu-id="1c069-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="1c069-142">Paramètres</span><span class="sxs-lookup"><span data-stu-id="1c069-142">Parameters</span></span></td>
            <td><span data-ttu-id="1c069-143">Spécifiez des paramètres de hello, si requis par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="1c069-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="1c069-144">Hello script tooinstall Giraph ne nécessite pas de paramètres, donc vous laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="1c069-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="1c069-145">Vous pouvez ajouter plusieurs tooinstall d’action de script de plusieurs composants sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1c069-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="1c069-146">Après avoir ajouté les scripts hello, cliquez sur toostart de coche hello création hello cluster.</span><span class="sxs-lookup"><span data-stu-id="1c069-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="1c069-147">Utiliser Giraph</span><span class="sxs-lookup"><span data-stu-id="1c069-147">Use Giraph</span></span>
<span data-ttu-id="1c069-148">Nous utilisons basic de hello hello SimpleShortestPathsComputation exemple toodemonstrate <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implémentation utilisée pour rechercher le chemin d’accès plus court de hello entre les objets dans un graphique.</span><span class="sxs-lookup"><span data-stu-id="1c069-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="1c069-149">Utilisez hello suivant les étapes tooupload hello exemple hello et les données exemple jar, exécuter une tâche à l’aide de hello SimpleShortestPathsComputation exemple, puis afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="1c069-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="1c069-150">Télécharger un tooAzure de fichier de données exemple stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="1c069-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="1c069-151">Sur votre poste de travail local, créez un nouveau fichier nommé **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="1c069-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="1c069-152">Elle doit contenir hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c069-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="1c069-153">Téléchargez hello tiny_graph.txt fichier toohello stockage principal pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c069-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="1c069-154">Pour obtenir des instructions sur la façon de tooupload de données, consultez [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="1c069-155">Ces données décrivant une relation entre les objets dans un graphique orienté, à l’aide du format de hello [source\_id, source\_valeur, [[destination\_id], [edge\_valeur],...]]. Chaque ligne représente une relation entre un objet **source\_id** et un ou plusieurs objets **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="1c069-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="1c069-156">Hello **bord\_valeur** (ou poids) peut être considéré comme puissance de hello ou de distance de connexion hello entre **source_id** et **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="1c069-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="1c069-157">Dessiner, à l’aide de valeur de hello (ou poids) en tant que la distance entre les objets hello, hello au-dessus de données peut se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c069-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="1c069-159">Exécutez hello SimpleShortestPathsComputation exemple.</span><span class="sxs-lookup"><span data-stu-id="1c069-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="1c069-160">Utilisez hello suivant toorun hello exemple Azure PowerShell applets de commande à l’aide du fichier de tiny_graph.txt hello en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="1c069-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1c069-161">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="1c069-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="1c069-162">étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1c069-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1c069-163">Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c069-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="1c069-164">Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1c069-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="1c069-165">Bonjour exemple ci-dessus, remplacez **clustername** avec nom hello de votre cluster HDInsight qui a Giraph installé.</span><span class="sxs-lookup"><span data-stu-id="1c069-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="1c069-166">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="1c069-166">View hello results.</span></span> <span data-ttu-id="1c069-167">Une fois terminé, les travaux hello hello résultats seront stockés dans deux fichiers de sortie Bonjour **wasb : / / / exemple/out/shotestpaths** dossier.</span><span class="sxs-lookup"><span data-stu-id="1c069-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="1c069-168">fichiers de Hello sont appelés **partie-m-00001** et **partie-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="1c069-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="1c069-169">Effectuez hello suivant les étapes toodownload et vue hello la sortie :</span><span class="sxs-lookup"><span data-stu-id="1c069-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="1c069-170">Cela créera hello **exemple/sortie/shortestpaths** structure du répertoire dans le répertoire en cours de hello sur votre station de travail et les fichiers toothat emplacement de téléchargement hello deux sortie.</span><span class="sxs-lookup"><span data-stu-id="1c069-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="1c069-171">Hello d’utilisation **Cat** contenu de hello toodisplay applet de commande des fichiers de hello :</span><span class="sxs-lookup"><span data-stu-id="1c069-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="1c069-172">une sortie Hello doit apparaître comme toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c069-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="1c069-173">Hello SimpleShortestPathComputation exemple est codé en dur toostart avec l’objet ID 1 et rechercher des objets de tooother hello plus courts chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="1c069-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="1c069-174">Afin de la sortie de hello doit être lu comme `destination_id distance`, où la distance est hello (ou valeur poids) des bords hello traversées entre l’objet ID 1 et ID hello cible.</span><span class="sxs-lookup"><span data-stu-id="1c069-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="1c069-175">Cette visualisation, vous pouvez vérifier les résultats hello par déplacement des chemins d’accès plus courts de hello entre l’ID 1 et tous les autres objets.</span><span class="sxs-lookup"><span data-stu-id="1c069-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="1c069-176">Notez que hello chemin le plus court entre les ID 1 et 4 de l’ID est 5.</span><span class="sxs-lookup"><span data-stu-id="1c069-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="1c069-177">Il s’agit hello total séparant <span style="color:orange">ID 1 et 3</span>, puis <span style="color:red">ID 3 et 4</span>.</span><span class="sxs-lookup"><span data-stu-id="1c069-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="1c069-179">Installation de Giraph à l'aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c069-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="1c069-180">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1c069-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="1c069-181">exemple Hello illustre comment tooinstall Spark à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c069-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="1c069-182">Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1c069-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="1c069-183">Installation de Giraph à l'aide de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1c069-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="1c069-184">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1c069-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="1c069-185">exemple Hello illustre comment tooinstall Spark à l’aide de hello du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="1c069-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="1c069-186">Vous devez toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1c069-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="1c069-187">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1c069-187">See also</span></span>
* [<span data-ttu-id="1c069-188">Installer Giraph sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="1c069-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="1c069-189">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c069-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="1c069-190">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="1c069-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="1c069-191">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="1c069-192">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark.</span><span class="sxs-lookup"><span data-stu-id="1c069-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="1c069-193">[Installer R sur les clusters HDInsight][hdinsight-install-r] : exemple d’action de script sur l’installation de R.</span><span class="sxs-lookup"><span data-stu-id="1c069-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="1c069-194">[Installation de Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md): exemple d’action de script sur l'installation de Solr.</span><span class="sxs-lookup"><span data-stu-id="1c069-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
