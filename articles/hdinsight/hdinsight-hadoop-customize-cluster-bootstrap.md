---
title: "aaaCustomize Clusters HDInsight à l’aide d’amorçage - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize HDInsight clusters à l’aide des données d’amorçage."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="9fddb-103">Personnalisation de clusters HDInsight à l’aide de Bootstrap</span><span class="sxs-lookup"><span data-stu-id="9fddb-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="9fddb-104">Parfois, vous souhaitez des fichiers de configuration de hello tooconfigure qui incluent :</span><span class="sxs-lookup"><span data-stu-id="9fddb-104">Sometimes, you want tooconfigure hello configuration files, which include:</span></span>

* <span data-ttu-id="9fddb-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="9fddb-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-106">core-site.xml</span></span>
* <span data-ttu-id="9fddb-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-107">gateway.xml</span></span>
* <span data-ttu-id="9fddb-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-108">hbase-env.xml</span></span>
* <span data-ttu-id="9fddb-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-109">hbase-site.xml</span></span>
* <span data-ttu-id="9fddb-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-110">hdfs-site.xml</span></span>
* <span data-ttu-id="9fddb-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-111">hive-env.xml</span></span>
* <span data-ttu-id="9fddb-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-112">hive-site.xml</span></span>
* <span data-ttu-id="9fddb-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="9fddb-113">mapred-site</span></span>
* <span data-ttu-id="9fddb-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-114">oozie-site.xml</span></span>
* <span data-ttu-id="9fddb-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-115">oozie-env.xml</span></span>
* <span data-ttu-id="9fddb-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-116">storm-site.xml</span></span>
* <span data-ttu-id="9fddb-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-117">tez-site.xml</span></span>
* <span data-ttu-id="9fddb-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-118">webhcat-site.xml</span></span>
* <span data-ttu-id="9fddb-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="9fddb-119">yarn-site.xml</span></span>

<span data-ttu-id="9fddb-120">Il existe trois méthodes toouse d’amorçage :</span><span class="sxs-lookup"><span data-stu-id="9fddb-120">There are three methods toouse bootstrap:</span></span>

* <span data-ttu-id="9fddb-121">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fddb-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="9fddb-122">Utilisation du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="9fddb-122">Use .NET SDK</span></span>
* <span data-ttu-id="9fddb-123">Utilisation d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9fddb-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="9fddb-124">Pour plus d’informations sur l’installation des composants supplémentaires sur le cluster HDInsight hello lors de la création, consultez :</span><span class="sxs-lookup"><span data-stu-id="9fddb-124">For information on installing additional components on HDInsight cluster during hello creation time, see:</span></span>

* [<span data-ttu-id="9fddb-125">Personnalisation des clusters HDInsight à l'aide d'une action de script (Linux)</span><span class="sxs-lookup"><span data-stu-id="9fddb-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="9fddb-126">Utilisation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fddb-126">Use Azure PowerShell</span></span>
<span data-ttu-id="9fddb-127">Hello suivant code PowerShell personnalise une configuration Hive :</span><span class="sxs-lookup"><span data-stu-id="9fddb-127">hello following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="9fddb-128">[L’annexe A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)décrit un script PowerShell complet.</span><span class="sxs-lookup"><span data-stu-id="9fddb-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="9fddb-129">**modification de hello tooverify :**</span><span class="sxs-lookup"><span data-stu-id="9fddb-129">**tooverify hello change:**</span></span>

1. <span data-ttu-id="9fddb-130">Ouverture de session toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9fddb-130">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9fddb-131">Dans le menu de gauche hello, cliquez sur **clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9fddb-131">From hello left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="9fddb-132">Si vous ne voyez pas cette option, cliquez d’abord sur **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="9fddb-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="9fddb-133">Cliquez sur le cluster hello que vous venez de créer à l’aide du script PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="9fddb-133">Click hello cluster you just created using hello PowerShell script.</span></span>
4. <span data-ttu-id="9fddb-134">Cliquez sur **tableau de bord** de haut hello de hello panneau tooopen hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="9fddb-134">Click **Dashboard** from hello top of hello blade tooopen hello Ambari UI.</span></span>
5. <span data-ttu-id="9fddb-135">Cliquez sur **la ruche** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="9fddb-135">Click **Hive** from hello left menu.</span></span>
6. <span data-ttu-id="9fddb-136">Sous **Résumé**, cliquez sur **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="9fddb-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="9fddb-137">Cliquez sur hello **configurations** onglet.</span><span class="sxs-lookup"><span data-stu-id="9fddb-137">Click hello **Configs** tab.</span></span>
8. <span data-ttu-id="9fddb-138">Cliquez sur **la ruche** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="9fddb-138">Click **Hive** from hello left menu.</span></span>
9. <span data-ttu-id="9fddb-139">Cliquez sur hello **avancé** onglet.</span><span class="sxs-lookup"><span data-stu-id="9fddb-139">Click hello **Advanced** tab.</span></span>
10. <span data-ttu-id="9fddb-140">Faites défiler vers le bas, puis développez **Site hive avancé**.</span><span class="sxs-lookup"><span data-stu-id="9fddb-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="9fddb-141">Recherchez **hive.metastore.client.socket.timeout** dans la section de hello.</span><span class="sxs-lookup"><span data-stu-id="9fddb-141">Look for **hive.metastore.client.socket.timeout** in hello section.</span></span>

<span data-ttu-id="9fddb-142">Et d’autres exemples sur la personnalisation d’autres fichiers de configuration :</span><span class="sxs-lookup"><span data-stu-id="9fddb-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="9fddb-143">Pour plus d’informations, consultez le blog d’Azim Uddin, intitulé [Personnalisation de la création d’un cluster HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fddb-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="9fddb-144">Utilisation du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="9fddb-144">Use .NET SDK</span></span>
<span data-ttu-id="9fddb-145">Consultez [basés sur Linux de créer des clusters HDInsight à l’aide hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="9fddb-145">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="9fddb-146">Utilisation d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9fddb-146">Use Resource Manager template</span></span>
<span data-ttu-id="9fddb-147">Vous pouvez utiliser Bootstrap dans un modèle Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="9fddb-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop personnalise le modèle Azure Resource Manager de Bootstrap de cluster](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="9fddb-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9fddb-149">See also</span></span>
* <span data-ttu-id="9fddb-150">[Créer des clusters Hadoop dans HDInsight] [ hdinsight-provision-cluster] fournit des instructions sur la façon dont toocreate un HDInsight de cluster à l’aide d’autres options personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9fddb-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="9fddb-151">[Développer des scripts d’action de script pour HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="9fddb-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="9fddb-152">[Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="9fddb-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="9fddb-153">[Installer et utiliser R sur les clusters HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="9fddb-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="9fddb-154">[Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="9fddb-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="9fddb-155">[Installez et utilisez Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9fddb-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Procédure de création d’un cluster"

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="9fddb-157">Annexe A : exemple PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fddb-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="9fddb-158">Ce script PowerShell permet de créer un cluster HDInsight et de personnaliser un paramètre Hive :</span><span class="sxs-lookup"><span data-stu-id="9fddb-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
