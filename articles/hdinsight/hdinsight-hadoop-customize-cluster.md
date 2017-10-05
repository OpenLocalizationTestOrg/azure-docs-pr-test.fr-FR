---
title: "Personnaliser des clusters HDInsight à l'aide d’actions de script - Azure | Documents Microsoft"
description: "Découvrez comment personnaliser des clusters HDInsight à l'aide d'une action de script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="24a6b-103">Personnalisation de clusters HDInsight basés sur Windows à l'aide d'une action de script</span><span class="sxs-lookup"><span data-stu-id="24a6b-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="24a6b-104">**action de script** peut être utilisée pour appeler des [scripts personnalisés](hdinsight-hadoop-script-actions.md) pendant le processus de création de cluster pour l’installation de logiciels supplémentaires sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="24a6b-105">Les informations présentes dans cet article sont spécifiques aux clusters HDInsight sous Windows.</span><span class="sxs-lookup"><span data-stu-id="24a6b-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="24a6b-106">Pour les clusters Linux, consultez la page [Personnaliser des clusters HDInsight Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="24a6b-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24a6b-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="24a6b-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="24a6b-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="24a6b-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="24a6b-109">Il est également possible de personnaliser les clusters HDInsight de bien d’autres façons, notamment en ajoutant des comptes de stockage supplémentaires, en modifiant les fichiers de configuration hadoop (core-site.xml, hive-site.xml, etc.) ou encore en ajoutant des bibliothèques partagées (comme Hive ou Oozie) dans des emplacements communs du cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="24a6b-110">Ces personnalisations peuvent être effectuées dans Azure PowerShell, le Kit de développement logiciel (SDK) Azure HDInsight .NET ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="24a6b-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="24a6b-111">Pour plus d’informations, consultez [Création de clusters Hadoop dans HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="24a6b-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="24a6b-112">Action de script dans le processus de création de cluster</span><span class="sxs-lookup"><span data-stu-id="24a6b-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="24a6b-113">L’action de script est utilisée uniquement pendant la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="24a6b-114">Le diagramme suivant illustre le moment de l’exécution de l’action de script pendant le processus de création :</span><span class="sxs-lookup"><span data-stu-id="24a6b-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="24a6b-115">![Personnalisation du cluster HDInsight et procédure de création d’un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="24a6b-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="24a6b-116">Quand le script est en cours d’exécution, le cluster entre dans la phase **ClusterCustomization** .</span><span class="sxs-lookup"><span data-stu-id="24a6b-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="24a6b-117">À ce stade, le script est exécuté sous le compte de l'administrateur système, en parallèle sur tous les nœuds spécifiés dans le cluster, et fournit des privilèges d'administrateur complets sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="24a6b-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="24a6b-118">Étant donné que vous disposez de privilèges d’administrateur sur les nœuds du cluster au cours de la phase **ClusterCustomization** , vous pouvez utiliser le script pour effectuer des opérations comme arrêter et démarrer des services, y compris des services liés à Hadoop.</span><span class="sxs-lookup"><span data-stu-id="24a6b-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="24a6b-119">Vous devez donc vous assurer, dans le cadre du script, que les services Ambari et autres services liés à Hadoop sont en cours d’exécution avant la fin de l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="24a6b-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="24a6b-120">Ces services sont requis pour établir correctement l'intégrité et l'état du cluster pendant sa création.</span><span class="sxs-lookup"><span data-stu-id="24a6b-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="24a6b-121">Si vous modifiez la configuration d'un cluster d'une manière qui affecte ces services, vous devez utiliser les fonctions d'assistance fournies.</span><span class="sxs-lookup"><span data-stu-id="24a6b-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="24a6b-122">Pour plus d’informations sur les fonctions d’assistance, consultez [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="24a6b-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="24a6b-123">La sortie et les journaux des erreurs du script sont stockés dans le compte de stockage par défaut spécifié pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="24a6b-124">Les journaux sont stockés dans une table nommée **u<\cluster-name-fragment><\time-stamp>setuplog**.</span><span class="sxs-lookup"><span data-stu-id="24a6b-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="24a6b-125">Il s’agit de journaux d’agrégation provenant du script exécuté sur tous les nœuds (nœud principal et nœuds de travail) dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="24a6b-126">Chaque cluster peut accepter plusieurs actions de script qui sont appelées dans l’ordre spécifié.</span><span class="sxs-lookup"><span data-stu-id="24a6b-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="24a6b-127">Un script peut être exécuté sur le nœud principal et/ou les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="24a6b-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="24a6b-128">HDInsight propose plusieurs scripts pour installer les composants suivants sur des clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="24a6b-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="24a6b-129">Nom</span><span class="sxs-lookup"><span data-stu-id="24a6b-129">Name</span></span> | <span data-ttu-id="24a6b-130">Script</span><span class="sxs-lookup"><span data-stu-id="24a6b-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="24a6b-131">**Installation de Spark**</span><span class="sxs-lookup"><span data-stu-id="24a6b-131">**Install Spark**</span></span> |<span data-ttu-id="24a6b-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="24a6b-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="24a6b-133">Consultez [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="24a6b-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="24a6b-134">**Installation de R**</span><span class="sxs-lookup"><span data-stu-id="24a6b-134">**Install R**</span></span> |<span data-ttu-id="24a6b-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="24a6b-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="24a6b-136">Consultez [Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="24a6b-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="24a6b-137">**Installation de Solr**</span><span class="sxs-lookup"><span data-stu-id="24a6b-137">**Install Solr**</span></span> |<span data-ttu-id="24a6b-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="24a6b-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="24a6b-139">Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="24a6b-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="24a6b-140">- **Installation de Giraph**</span><span class="sxs-lookup"><span data-stu-id="24a6b-140">- **Install Giraph**</span></span> |<span data-ttu-id="24a6b-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="24a6b-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="24a6b-142">Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="24a6b-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="24a6b-143">**Précharger les bibliothèques Hive**</span><span class="sxs-lookup"><span data-stu-id="24a6b-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="24a6b-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="24a6b-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="24a6b-145">Consultez [Ajouter des bibliothèques Hive sur des clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="24a6b-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="24a6b-146">Appel de scripts à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="24a6b-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="24a6b-147">**Dans le portail Azure**</span><span class="sxs-lookup"><span data-stu-id="24a6b-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="24a6b-148">Démarrez la création d'un cluster comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="24a6b-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="24a6b-149">Dans Configuration facultative, sur le panneau **Actions de script**, cliquez sur **ajouter l’action de script** pour fournir des informations sur l’action de script, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="24a6b-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="24a6b-150">![Utiliser Action de script pour personnaliser un cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Utiliser Action de script pour personnaliser un cluster")</span><span class="sxs-lookup"><span data-stu-id="24a6b-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="24a6b-151">Propriété</span><span class="sxs-lookup"><span data-stu-id="24a6b-151">Property</span></span></th><th><span data-ttu-id="24a6b-152">Valeur</span><span class="sxs-lookup"><span data-stu-id="24a6b-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="24a6b-153">Nom</span><span class="sxs-lookup"><span data-stu-id="24a6b-153">Name</span></span></td>
            <td><span data-ttu-id="24a6b-154">Indiquez un nom pour l'action de script.</span><span class="sxs-lookup"><span data-stu-id="24a6b-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="24a6b-155">URI du script</span><span class="sxs-lookup"><span data-stu-id="24a6b-155">Script URI</span></span></td>
            <td><span data-ttu-id="24a6b-156">Spécifiez l'URI du script appelé pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="24a6b-157">s</span><span class="sxs-lookup"><span data-stu-id="24a6b-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="24a6b-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="24a6b-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="24a6b-159">Spécifiez les nœuds (**Head** ou **Worker**) sur lesquels le script de personnalisation est exécuté. </b>.</span><span class="sxs-lookup"><span data-stu-id="24a6b-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="24a6b-160">parameters</span><span class="sxs-lookup"><span data-stu-id="24a6b-160">Parameters</span></span></td>
            <td><span data-ttu-id="24a6b-161">Spécifiez les paramètres, si le script le demande.</span><span class="sxs-lookup"><span data-stu-id="24a6b-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="24a6b-162">Appuyez sur ENTRÉE pour ajouter plusieurs actions de script et installer plusieurs composants sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="24a6b-163">Cliquez sur **Sélectionner** pour enregistrer la configuration d’action de script et poursuivre la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="24a6b-164">Appel de scripts à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="24a6b-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="24a6b-165">Le script PowerShell suivant montre comment installer Spark sur un cluster HDInsight basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="24a6b-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="24a6b-166">Pour installer d'autres logiciels, vous devrez remplacer le fichier de script dans le script :</span><span class="sxs-lookup"><span data-stu-id="24a6b-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="24a6b-167">Lorsque vous y êtes invité, entrez les informations d'identification du cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="24a6b-168">La création du cluster peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="24a6b-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="24a6b-169">Appel de scripts à l'aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="24a6b-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="24a6b-170">L’exemple suivant montre comment installer Spark sur un cluster HDInsight basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="24a6b-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="24a6b-171">Pour installer d'autres logiciels, vous devrez remplacer le fichier de script dans le code.</span><span class="sxs-lookup"><span data-stu-id="24a6b-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="24a6b-172">**Pour créer un cluster HDInsight avec Spark**</span><span class="sxs-lookup"><span data-stu-id="24a6b-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="24a6b-173">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24a6b-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="24a6b-174">À partir de la console du gestionnaire de package Nuget, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="24a6b-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="24a6b-175">Utilisez les instructions using suivantes dans le fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="24a6b-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="24a6b-176">Placez le code dans la classe en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="24a6b-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="24a6b-177">Appuyez sur **F5** pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="24a6b-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="24a6b-178">Prise en charge des logiciels open source utilisés sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="24a6b-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="24a6b-179">Le service Microsoft Azure HDInsight est une plateforme flexible qui vous permet de créer des applications de données volumineuses (Big Data) dans le cloud à l’aide d’un écosystème de technologies open source articulées autour de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="24a6b-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="24a6b-180">Microsoft Azure fournit un niveau de support général pour les technologies open source, comme indiqué dans la section **Portée du support** du site web <a href="http://azure.microsoft.com/support/faq/" target="_blank">FAQ du support Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="24a6b-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="24a6b-181">Le service HDInsight fournit un niveau de support supplémentaire pour certains composants, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="24a6b-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="24a6b-182">Deux types de composant open source sont disponibles dans le service HDInsight :</span><span class="sxs-lookup"><span data-stu-id="24a6b-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="24a6b-183">**Composants intégrés** : ces composants sont préinstallés sur les clusters HDInsight et fournissent la fonctionnalité principale du cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="24a6b-184">Par exemple, YARN ResourceManager, le langage de requête Hive (HiveQL) et la bibliothèque Mahout appartiennent à cette catégorie.</span><span class="sxs-lookup"><span data-stu-id="24a6b-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="24a6b-185">Une liste complète des composants de cluster est disponible sur la page [Nouveautés des versions de cluster Hadoop fournies par HDInsight](hdinsight-component-versioning.md)</a>.</span><span class="sxs-lookup"><span data-stu-id="24a6b-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="24a6b-186">**Composants personnalisés** : en tant qu’utilisateur du cluster, vous pouvez installer ou utiliser, dans votre charge de travail, tout composant qui est disponible dans la communauté ou que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="24a6b-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="24a6b-187">Les composants intégrés bénéficient d’une prise en charge totale, et le support Microsoft vous aidera à identifier et à résoudre les problèmes liés à ces composants.</span><span class="sxs-lookup"><span data-stu-id="24a6b-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="24a6b-188">Les composants fournis avec le cluster HDInsight bénéficient d’une prise en charge totale, et le support Microsoft vous aidera à identifier et à résoudre les problèmes liés à ces composants.</span><span class="sxs-lookup"><span data-stu-id="24a6b-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="24a6b-189">Les composants personnalisés bénéficient d'un support commercialement raisonnable pour vous aider à résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="24a6b-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="24a6b-190">Cela signifie SOIT que le problème pourra être résolu, SOIT que vous serez invité à affecter les ressources disponibles pour les technologies Open Source.</span><span class="sxs-lookup"><span data-stu-id="24a6b-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="24a6b-191">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="24a6b-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="24a6b-192">En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org) ; par exemple, [Hadoop](http://hadoop.apache.org/) ou [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="24a6b-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="24a6b-193">Le service HDInsight fournit plusieurs méthodes d’utilisation de ces composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="24a6b-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="24a6b-194">Quel que soit le mode d’utilisation ou d’installation du composant sur le cluster, le même niveau de support s’applique.</span><span class="sxs-lookup"><span data-stu-id="24a6b-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="24a6b-195">Vous trouverez, ci-dessous, la liste des méthodes les plus courantes d’utilisation des composants personnalisés sur des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="24a6b-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="24a6b-196">Envoi de travaux : il est possible d’envoyer des travaux Hadoop ou d’autres types de travaux au cluster qui exécute ou utilise des composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="24a6b-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="24a6b-197">Personnalisation de cluster : lors de la création du cluster, vous pouvez spécifier des paramètres supplémentaires et des composants personnalisés qui seront installés sur les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="24a6b-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="24a6b-198">Exemples : pour des composants personnalisés fréquemment utilisés, il arrive que Microsoft et d’autres éditeurs proposent des exemples illustrant leur utilisation sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="24a6b-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="24a6b-199">Ces exemples sont fournis sans support.</span><span class="sxs-lookup"><span data-stu-id="24a6b-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="24a6b-200">Développer des scripts d’action de script</span><span class="sxs-lookup"><span data-stu-id="24a6b-200">Develop Script Action scripts</span></span>
<span data-ttu-id="24a6b-201">Consultez [Développer des scripts d’action de script pour HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="24a6b-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="24a6b-202">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="24a6b-202">See also</span></span>
* <span data-ttu-id="24a6b-203">[Créer des clusters Hadoop dans HDInsight][hdinsight-provision-cluster] pour obtenir des instructions sur la création d’un cluster HDInsight à l’aide d’autres options personnalisées.</span><span class="sxs-lookup"><span data-stu-id="24a6b-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="24a6b-204">[Développer des scripts d’action de script pour HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="24a6b-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="24a6b-205">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="24a6b-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="24a6b-206">[Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="24a6b-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="24a6b-207">[Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="24a6b-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="24a6b-208">[Installez et utilisez Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="24a6b-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="24a6b-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Procédure de création d’un cluster"</span><span class="sxs-lookup"><span data-stu-id="24a6b-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
