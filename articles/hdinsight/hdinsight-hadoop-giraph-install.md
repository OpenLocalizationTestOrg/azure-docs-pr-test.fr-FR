---
title: Installer et utiliser Giraph sur des clusters Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment personnaliser un cluster HDInsight avec Giraph et comment utiliser Giraph."
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
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="8644d-103">Installer et utiliser Giraph sur les clusters HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="8644d-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="8644d-104">Découvrez comment personnaliser un cluster HDInsight basé sur Windows avec Giraph à l’aide d’une action de script, et comment utiliser Giraph pour traiter des graphiques à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="8644d-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="8644d-105">Pour plus d’informations sur l’utilisation de Giraph avec un cluster Linux, consultez [Installation de Giraph sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8644d-106">Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="8644d-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="8644d-107">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="8644d-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="8644d-108">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="8644d-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8644d-109">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8644d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="8644d-110">Pour plus d’informations sur l’installation de Giraph sur un cluster HDInsight Linux, consultez [Installer Giraph sur des clusters HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="8644d-111">Vous pouvez installer Giraph sur n’importe quel type de cluster (Hadoop, Storm, HBase, Spark) sur Azure HDInsight à l’aide d’une *action de script*.</span><span class="sxs-lookup"><span data-stu-id="8644d-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="8644d-112">Pour obtenir un exemple de script pour installer Giraph sur un cluster HDInsight, téléchargez l’objet blob de stockage Azure en lecture seule à l’adresse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="8644d-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="8644d-113">L'exemple de script fonctionne uniquement avec un cluster HDInsight version 3.1.</span><span class="sxs-lookup"><span data-stu-id="8644d-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="8644d-114">Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="8644d-115">**Articles connexes**</span><span class="sxs-lookup"><span data-stu-id="8644d-115">**Related articles**</span></span>

* [<span data-ttu-id="8644d-116">Installer Giraph sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="8644d-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="8644d-117">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8644d-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="8644d-118">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="8644d-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="8644d-119">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="8644d-120">Présentation de Giraph</span><span class="sxs-lookup"><span data-stu-id="8644d-120">What is Giraph?</span></span>
<span data-ttu-id="8644d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permet de traiter des graphiques avec Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8644d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="8644d-122">Les graphiques modélisent les relations entre les objets, telles que les connexions entre routeurs sur un grand réseau comme Internet ou les relations entre individus sur les réseaux sociaux (parfois appelés graphiques sociaux).</span><span class="sxs-lookup"><span data-stu-id="8644d-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="8644d-123">Le traitement des graphiques permet d'examiner les relations entre les objets d'un graphique, par exemple :</span><span class="sxs-lookup"><span data-stu-id="8644d-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="8644d-124">identifier les amis potentiels en fonction de vos relations actuelles ;</span><span class="sxs-lookup"><span data-stu-id="8644d-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="8644d-125">identifier le chemin le plus court entre deux ordinateurs d'un réseau ;</span><span class="sxs-lookup"><span data-stu-id="8644d-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="8644d-126">calculer le classement de pages web.</span><span class="sxs-lookup"><span data-stu-id="8644d-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="8644d-127">Installation de Giraph à l'aide du portail</span><span class="sxs-lookup"><span data-stu-id="8644d-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="8644d-128">Démarrez la création d’un cluster à l’aide de l’option **CRÉATION PERSONNALISÉE** , comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="8644d-129">Sur la page **Actions de script** de l’Assistant, cliquez sur **ajouter l’action de script** pour fournir des informations sur l’action de script, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8644d-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="8644d-130">![Utiliser Action de script pour personnaliser un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Utiliser Action de script pour personnaliser un cluster")</span><span class="sxs-lookup"><span data-stu-id="8644d-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="8644d-131">Propriété</span><span class="sxs-lookup"><span data-stu-id="8644d-131">Property</span></span></th><th><span data-ttu-id="8644d-132">Valeur</span><span class="sxs-lookup"><span data-stu-id="8644d-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="8644d-133">Nom</span><span class="sxs-lookup"><span data-stu-id="8644d-133">Name</span></span></td>
            <td><span data-ttu-id="8644d-134">Indiquez un nom pour l'action de script.</span><span class="sxs-lookup"><span data-stu-id="8644d-134">Specify a name for the script action.</span></span> <span data-ttu-id="8644d-135">Par exemple, <b>Installation Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="8644d-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="8644d-136">URI du script</span><span class="sxs-lookup"><span data-stu-id="8644d-136">Script URI</span></span></td>
            <td><span data-ttu-id="8644d-137">Spécifiez l'URI (Uniform Resource Identifier) du script appelé pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="8644d-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="8644d-138">Par exemple, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="8644d-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="8644d-139">Type de nœud</span><span class="sxs-lookup"><span data-stu-id="8644d-139">Node Type</span></span></td>
            <td><span data-ttu-id="8644d-140">Spécifiez les nœuds sur lesquels le script de personnalisation est exécuté.</span><span class="sxs-lookup"><span data-stu-id="8644d-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="8644d-141">Vous avez le choix entre <b>Tous les nœuds</b>, <b>Nœuds principaux uniquement</b> et <b>Nœuds de travail uniquement</b>.</span><span class="sxs-lookup"><span data-stu-id="8644d-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="8644d-142">parameters</span><span class="sxs-lookup"><span data-stu-id="8644d-142">Parameters</span></span></td>
            <td><span data-ttu-id="8644d-143">Spécifiez les paramètres, si le script le demande.</span><span class="sxs-lookup"><span data-stu-id="8644d-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="8644d-144">Le script d'installation de Giraph ne nécessite aucun paramètre. Vous pouvez donc laisser ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="8644d-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="8644d-145">Vous pouvez ajouter plusieurs actions de script pour installer plusieurs composants sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="8644d-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="8644d-146">Après avoir ajouté les scripts, cliquez sur la coche pour démarrer la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="8644d-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="8644d-147">Utiliser Giraph</span><span class="sxs-lookup"><span data-stu-id="8644d-147">Use Giraph</span></span>
<span data-ttu-id="8644d-148">L’exemple SimpleShortestPathsComputation indique l’implémentation basique de <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> pour trouver le chemin le plus court entre des objets d’un graphique.</span><span class="sxs-lookup"><span data-stu-id="8644d-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="8644d-149">Procédez comme suit pour télécharger les exemples de données et l'exemple de fichier JAR, exécuter une tâche avec l'exemple SimpleShortestPathsComputation, puis afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="8644d-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="8644d-150">Téléchargez un exemple de fichier de données dans le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8644d-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="8644d-151">Sur votre poste de travail local, créez un nouveau fichier nommé **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="8644d-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="8644d-152">Il doit contenir les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8644d-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="8644d-153">Téléchargez le fichier tiny_graph.txt dans le stockage principal pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8644d-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="8644d-154">Pour plus d’informations sur le téléchargement de données, consultez la rubrique [Téléchargement de données pour les tâches Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="8644d-155">Ces données décrivent une relation entre les objets d’un graphique dirigé, en utilisant le format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span><span class="sxs-lookup"><span data-stu-id="8644d-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="8644d-156">Chaque ligne représente une relation entre un objet **source\_id** et un ou plusieurs objets **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="8644d-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="8644d-157">La valeur **edge\_value** (ou pondération) peut être considérée comme l’intensité ou la distance de la connexion entre **source_id** et **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="8644d-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="8644d-158">Dessinées en utilisant la valeur (ou la pondération) comme la distance entre les objets, les données ci-dessus peuvent ressembler à cela :</span><span class="sxs-lookup"><span data-stu-id="8644d-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="8644d-160">Exécutez l'exemple SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="8644d-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="8644d-161">Utilisez les applets de commande Azure PowerShell suivantes pour exécuter l'exemple en utilisant le fichier tiny_graph.txt comme entrée.</span><span class="sxs-lookup"><span data-stu-id="8644d-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8644d-162">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="8644d-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="8644d-163">Dans ce document, la procédure repose sur les nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8644d-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="8644d-164">Suivez les étapes indiquées dans [Installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs) pour installer la dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8644d-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="8644d-165">Si vous devez modifier certains scripts pour utiliser les nouvelles applets de commande fonctionnant avec Azure Resource Manager, consultez [Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8644d-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="8644d-166">Dans l’exemple ci-dessus, remplacez **clustername** par le nom de votre cluster HDInsight sur lequel Giraph est installé.</span><span class="sxs-lookup"><span data-stu-id="8644d-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="8644d-167">Affichez les résultats.</span><span class="sxs-lookup"><span data-stu-id="8644d-167">View the results.</span></span> <span data-ttu-id="8644d-168">Une fois la tâche terminée, les résultats sont stockés dans deux fichiers de sortie, dans le dossier **wasb:///example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="8644d-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="8644d-169">Les fichiers se nomment **part-m-00001** et **part-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="8644d-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="8644d-170">Procédez comme suit pour télécharger et afficher le résultat :</span><span class="sxs-lookup"><span data-stu-id="8644d-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="8644d-171">Cette opération crée la structure de répertoires **example/output/shortestpaths** dans le répertoire actuel de votre poste de travail et télécharge les deux fichiers de sortie à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="8644d-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="8644d-172">Utilisez l’applet de commande **Cat** pour afficher le contenu des fichiers :</span><span class="sxs-lookup"><span data-stu-id="8644d-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="8644d-173">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8644d-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="8644d-174">L'exemple SimpleShortestPathComputation est codé en dur de façon à commencer avec l'ID d'objet 1 et trouver le chemin le plus court vers les autres objets.</span><span class="sxs-lookup"><span data-stu-id="8644d-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="8644d-175">Le résultat doit être lu comme `destination_id distance`, où distance est la valeur (ou la pondération) des bords parcourus entre l’ID d’objet 1 et l’ID cible.</span><span class="sxs-lookup"><span data-stu-id="8644d-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="8644d-176">En visualisant cela, vous pouvez vérifier les résultats en parcourant les chemins les plus courts entre l'ID 1 et tous les autres objets.</span><span class="sxs-lookup"><span data-stu-id="8644d-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="8644d-177">Notez que le chemin le plus court entre ID 1 et ID 4 est 5.</span><span class="sxs-lookup"><span data-stu-id="8644d-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="8644d-178">Il s’agit de la distance totale entre <span style="color:orange">ID 1 et 3</span>, puis entre <span style="color:red">ID 3 et 4</span>.</span><span class="sxs-lookup"><span data-stu-id="8644d-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="8644d-180">Installation de Giraph à l'aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8644d-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="8644d-181">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="8644d-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="8644d-182">L'exemple montre comment installer Spark avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8644d-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="8644d-183">Vous devez personnaliser le script pour utiliser [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="8644d-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="8644d-184">Installation de Giraph à l'aide de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8644d-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="8644d-185">Consultez [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="8644d-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="8644d-186">L'exemple montre comment installer Spark à l'aide du Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="8644d-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="8644d-187">Vous devez personnaliser le script pour utiliser [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="8644d-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="8644d-188">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8644d-188">See also</span></span>
* [<span data-ttu-id="8644d-189">Installer Giraph sur des clusters HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="8644d-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="8644d-190">[Créer des clusters Hadoop dans HDInsight](hdinsight-provision-clusters.md): informations générales sur la création de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8644d-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="8644d-191">[Personnaliser un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize] : informations générales sur la personnalisation de clusters HDInsight à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="8644d-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="8644d-192">[Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="8644d-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="8644d-193">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark] : exemple d’action de script sur l’installation de Spark.</span><span class="sxs-lookup"><span data-stu-id="8644d-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="8644d-194">[Installer R sur les clusters HDInsight][hdinsight-install-r] : exemple d’action de script sur l’installation de R.</span><span class="sxs-lookup"><span data-stu-id="8644d-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="8644d-195">[Installation de Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md): exemple d’action de script sur l'installation de Solr.</span><span class="sxs-lookup"><span data-stu-id="8644d-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
