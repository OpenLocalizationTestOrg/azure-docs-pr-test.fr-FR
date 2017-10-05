---
title: "Migrer vers les outils de développement Azure Resource Manager pour HDInsight | Microsoft Docs"
description: "Procédure de migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="e2148-103">Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2148-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="e2148-104">HDInsight déconseille les outils Azure Service Manager (ASM) pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2148-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="e2148-105">Si vous avez utilisé Azure PowerShell, l’interface de ligne de commande Azure ou le SDK .NET HDInsight pour travailler avec les clusters HDInsight, nous vous invitons désormais à utiliser les versions Azure Resource Manager (ARM) de PowerShell, de l’interface de ligne de commande et du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="e2148-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="e2148-106">Cet article fournit des repères sur la façon de migrer vers la nouvelle approche ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="e2148-107">Cet article souligne également, le cas échéant, les différences entre les approches ASM et ARM pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2148-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2148-108">La prise en charge de PowerShell, de l’interface de ligne de commande et du SDK .NET ASM sera interrompue le **1er janvier 2017**.</span><span class="sxs-lookup"><span data-stu-id="e2148-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="e2148-109">Utilisation de l’interface de ligne de commande Azure vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e2148-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="e2148-110">L’interface de ligne de commande Azure est maintenant en mode Azure Resource Manager (ARM) par défaut, sauf si vous mettez à niveau à partir d’une installation précédente. Dans ce cas, vous devrez peut-être utiliser la commande `azure config mode arm` pour passer en mode ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="e2148-111">Les commandes de base que l’interface de ligne de commande Azure a fournies pour fonctionner avec HDInsight à l’aide d’Azure Service Management (ASM) sont identiques lors de l’utilisation d’ARM. Toutefois, certains paramètres et commutateurs peuvent avoir des nouveaux noms, et de nombreux nouveaux paramètres sont disponibles lorsque vous utilisez ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="e2148-112">Par exemple, vous pouvez maintenant utiliser `azure hdinsight cluster create` pour spécifier le réseau virtuel Azure dans lequel un cluster devrait être créé, ou des informations sur les metastores Hive et Oozie.</span><span class="sxs-lookup"><span data-stu-id="e2148-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="e2148-113">Les commandes de base pour travailler avec HDInsight via le Azure Resource Manager sont :</span><span class="sxs-lookup"><span data-stu-id="e2148-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="e2148-114">`azure hdinsight cluster create` - crée un nouveau cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2148-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="e2148-115">`azure hdinsight cluster delete` - supprime un cluster HDInsight existant</span><span class="sxs-lookup"><span data-stu-id="e2148-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="e2148-116">`azure hdinsight cluster show` -affiche des informations sur un cluster existant</span><span class="sxs-lookup"><span data-stu-id="e2148-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="e2148-117">`azure hdinsight cluster list` - répertorie les clusters HDInsight pour votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="e2148-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="e2148-118">Utilisez le commutateur `-h` pour inspecter les paramètres et les commutateurs disponibles pour chaque commande.</span><span class="sxs-lookup"><span data-stu-id="e2148-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="e2148-119">Nouvelles commandes</span><span class="sxs-lookup"><span data-stu-id="e2148-119">New commands</span></span>
<span data-ttu-id="e2148-120">Les nouvelles commandes disponibles avec Azure Resource Manager sont :</span><span class="sxs-lookup"><span data-stu-id="e2148-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="e2148-121">`azure hdinsight cluster resize` -modifie de manière dynamique le nombre de nœuds worker dans le cluster</span><span class="sxs-lookup"><span data-stu-id="e2148-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="e2148-122">`azure hdinsight cluster enable-http-access` - active l’accès HTTPs au cluster (activé par défaut)</span><span class="sxs-lookup"><span data-stu-id="e2148-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="e2148-123">`azure hdinsight cluster disable-http-access` - désactive l’accès HTTPs au cluster</span><span class="sxs-lookup"><span data-stu-id="e2148-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="e2148-124">`azure hdinsight script-action` - fournit des commandes pour créer/gérer des actions de script sur un cluster</span><span class="sxs-lookup"><span data-stu-id="e2148-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="e2148-125">`azure hdinsight config` - fournit des commandes pour créer un fichier de configuration qui peut être utilisé avec la commande `hdinsight cluster create` pour fournir des informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="e2148-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="e2148-126">Commandes déconseillées</span><span class="sxs-lookup"><span data-stu-id="e2148-126">Deprecated commands</span></span>
<span data-ttu-id="e2148-127">Si vous utilisez les commandes `azure hdinsight job` pour envoyer des travaux vers votre cluster HDInsight, ceux-ci ne sont pas disponibles via les commandes ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="e2148-128">Si vous devez envoyer des travaux par programme vers HDInsight à partir de scripts, vous devez à la place utiliser les API REST fournies par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2148-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="e2148-129">Pour plus d’informations sur l’envoi de travaux à l’aide des API REST, consultez les documents suivants.</span><span class="sxs-lookup"><span data-stu-id="e2148-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="e2148-130">Exécution à distance des tâches MapReduce avec Hadoop sur HDInsight à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="e2148-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="e2148-131">Exécution de requêtes Hive avec Hadoop dans HDInsight via Curl</span><span class="sxs-lookup"><span data-stu-id="e2148-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="e2148-132">Exécution à distance des tâches Pig avec Hadoop sur HDInsight à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="e2148-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="e2148-133">Pour plus d’informations sur d’autres méthodes d’exécution interactive de MapReduce, Hive et Pig, consultez [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md), [Utilisation de Hive avec Hadoop dans HDInsight](hdinsight-use-hive.md) et [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="e2148-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="e2148-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="e2148-134">Examples</span></span>
<span data-ttu-id="e2148-135">**Création d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-135">**Creating a cluster**</span></span>

* <span data-ttu-id="e2148-136">Ancienne commande (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="e2148-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="e2148-137">Nouvelle commande (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="e2148-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="e2148-138">**Suppression d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="e2148-139">Ancienne commande (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="e2148-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="e2148-140">Nouvelle commande (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="e2148-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="e2148-141">**Énumérer les clusters**</span><span class="sxs-lookup"><span data-stu-id="e2148-141">**List clusters**</span></span>

* <span data-ttu-id="e2148-142">Ancienne commande (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="e2148-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="e2148-143">Nouvelle commande (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="e2148-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="e2148-144">Pour la commande list, le fait de spécifier le groupe de ressources à l’aide de `-g` renvoie uniquement les clusters dans le groupe de ressources spécifié.</span><span class="sxs-lookup"><span data-stu-id="e2148-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="e2148-145">**Afficher les informations du cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-145">**Show cluster information**</span></span>

* <span data-ttu-id="e2148-146">Ancienne commande (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="e2148-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="e2148-147">Nouvelle commande (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="e2148-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="e2148-148">Migration d’Azure PowerShell vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e2148-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="e2148-149">Les informations générales concernant Azure PowerShell en mode Azure Resource Manager (ARM) sont disponibles dans la page [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e2148-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="e2148-150">Les applets de commande Azure PowerShell ARM peuvent être installées côte à côte avec les applets de commande ASM.</span><span class="sxs-lookup"><span data-stu-id="e2148-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="e2148-151">Les applets de commande des deux modes se distinguent par leurs noms.</span><span class="sxs-lookup"><span data-stu-id="e2148-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="e2148-152">Le mode ARM a *AzureRmHDInsight* dans les noms d’applets de commande au lieu de *AzureHDInsight* en mode ASM.</span><span class="sxs-lookup"><span data-stu-id="e2148-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="e2148-153">Par exemple, *New-AzureRmHDInsightCluster* et *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="e2148-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="e2148-154">Toutefois, certains paramètres et commutateurs peuvent avoir des nouveaux noms, et de nombreux nouveaux paramètres sont disponibles lorsque vous utilisez ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="e2148-155">Par exemple, plusieurs applets de commande exigent un nouveau commutateur appelé *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="e2148-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="e2148-156">Avant de pouvoir utiliser les applets de commande HDInsight, vous devez vous connecter à votre compte Azure et créer un nouveau groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="e2148-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="e2148-157">Login-AzureRmAccount ou [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2148-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="e2148-158">Consultez [Authentification d’un principal du service à l’aide d’Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="e2148-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="e2148-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2148-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="e2148-160">Applets de commande renommées</span><span class="sxs-lookup"><span data-stu-id="e2148-160">Renamed cmdlets</span></span>
<span data-ttu-id="e2148-161">Pour répertorier les applets de commande HDInsight ASM dans la console Windows PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e2148-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="e2148-162">Le tableau suivant répertorie les applets de commande ASM et leurs noms en mode ARM :</span><span class="sxs-lookup"><span data-stu-id="e2148-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="e2148-163">Applets de commande ASM</span><span class="sxs-lookup"><span data-stu-id="e2148-163">ASM cmdlets</span></span> | <span data-ttu-id="e2148-164">Applets de commande ARM</span><span class="sxs-lookup"><span data-stu-id="e2148-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="e2148-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="e2148-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="e2148-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="e2148-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="e2148-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="e2148-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="e2148-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="e2148-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="e2148-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="e2148-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="e2148-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="e2148-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="e2148-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="e2148-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="e2148-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="e2148-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="e2148-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e2148-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="e2148-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="e2148-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="e2148-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="e2148-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="e2148-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="e2148-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="e2148-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="e2148-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="e2148-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="e2148-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="e2148-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="e2148-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="e2148-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="e2148-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="e2148-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="e2148-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="e2148-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="e2148-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="e2148-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e2148-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="e2148-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="e2148-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="e2148-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="e2148-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="e2148-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="e2148-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="e2148-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="e2148-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="e2148-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="e2148-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="e2148-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="e2148-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="e2148-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="e2148-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="e2148-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="e2148-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e2148-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="e2148-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="e2148-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="e2148-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="e2148-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="e2148-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="e2148-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="e2148-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="e2148-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="e2148-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="e2148-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="e2148-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="e2148-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="e2148-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="e2148-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="e2148-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="e2148-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="e2148-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="e2148-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="e2148-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="e2148-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="e2148-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="e2148-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="e2148-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="e2148-219">Nouvelles applets de commande</span><span class="sxs-lookup"><span data-stu-id="e2148-219">New cmdlets</span></span>
<span data-ttu-id="e2148-220">Les nouvelles applets de commande suivantes sont uniquement disponibles en mode ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="e2148-221">**Applets de commandes associées à une action de script :**</span><span class="sxs-lookup"><span data-stu-id="e2148-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="e2148-222">**Get-AzureRmHDInsightPersistedScriptAction**: obtient les actions de script persistantes pour un cluster et les répertorie par ordre chronologique ou obtient des informations pour une action de script persistante spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e2148-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="e2148-223">**Get-AzureRmHDInsightScriptActionHistory**: obtient l’historique d’actions de script pour un cluster et les répertorie par ordre chronologique inversé, ou obtient des informations d’une action de script exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="e2148-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="e2148-224">**Remove-AzureRmHDInsightPersistedScriptAction**: retire une action de script persistante d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2148-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="e2148-225">**Set-AzureRmHDInsightPersistedScriptAction**: définit une action de script exécutée précédemment comme action de script persistante.</span><span class="sxs-lookup"><span data-stu-id="e2148-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="e2148-226">**Submit-AzureRmHDInsightScriptAction**: envoie une nouvelle action de script vers un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2148-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="e2148-227">Pour plus d’informations sur l’utilisation, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e2148-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="e2148-228">**Applets de commande associées à l’identité du cluster :**</span><span class="sxs-lookup"><span data-stu-id="e2148-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="e2148-229">**Add-AzureRmHDInsightClusterIdentity**: ajoute une identité de cluster à un objet configuration de cluster pour que le cluster HDInsight puisse accéder à Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e2148-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="e2148-230">Consultez la page [Créer un cluster HDInsight avec Data Lake Store à l’aide d’Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e2148-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="e2148-231">Exemples</span><span class="sxs-lookup"><span data-stu-id="e2148-231">Examples</span></span>
<span data-ttu-id="e2148-232">**Créer un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-232">**Create cluster**</span></span>

<span data-ttu-id="e2148-233">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="e2148-234">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="e2148-235">**Supprimer un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-235">**Delete cluster**</span></span>

<span data-ttu-id="e2148-236">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="e2148-237">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="e2148-238">**Répertorier un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-238">**List cluster**</span></span>

<span data-ttu-id="e2148-239">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="e2148-240">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="e2148-241">**Afficher le cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-241">**Show cluster**</span></span>

<span data-ttu-id="e2148-242">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="e2148-243">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="e2148-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="e2148-244">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="e2148-244">Other samples</span></span>
* [<span data-ttu-id="e2148-245">Création de clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2148-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="e2148-246">Envoi de tâches Hive</span><span class="sxs-lookup"><span data-stu-id="e2148-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="e2148-247">Envoi de tâches Pig</span><span class="sxs-lookup"><span data-stu-id="e2148-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="e2148-248">Envoi de tâches Sqoop</span><span class="sxs-lookup"><span data-stu-id="e2148-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="e2148-249">Migration vers le Kit de développement logiciel (SDK) .NET HDInsight ARM</span><span class="sxs-lookup"><span data-stu-id="e2148-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="e2148-250">Le [Kit de développement logiciel (SDK) .NET HDInsight (ASM)](https://msdn.microsoft.com/library/azure/mt416619.aspx) Azure Service Management est maintenant déconseillé.</span><span class="sxs-lookup"><span data-stu-id="e2148-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="e2148-251">Nous vous invitons à utiliser le [Kit de développement logiciel (SDK) .NET HDInsight (ARM)](https://msdn.microsoft.com/library/azure/mt271028.aspx)Azure Resource Management.</span><span class="sxs-lookup"><span data-stu-id="e2148-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="e2148-252">Les packages HDInsight ASM suivants sont désormais déconseillés.</span><span class="sxs-lookup"><span data-stu-id="e2148-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="e2148-253">Cette section fournit des liens vers des informations supplémentaires sur la façon d’effectuer certaines tâches à l’aide du Kit de développement logiciel (SDK) ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="e2148-254">Procédure d’utilisation du Kit de développement logiciel (SDK) .NET HDInsight ARM</span><span class="sxs-lookup"><span data-stu-id="e2148-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="e2148-255">Liens</span><span class="sxs-lookup"><span data-stu-id="e2148-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="e2148-256">Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-257">Consultez [Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="e2148-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e2148-258">Personnaliser un cluster à l’aide d’une action de script avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="e2148-259">Consultez [Personnaliser des clusters HDInsight sous Linux à l’aide d’une action de script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="e2148-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="e2148-260">Authentifier des applications de manière interactive à l’aide d’Azure Active Directory avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="e2148-261">Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e2148-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="e2148-262">Dans cet article, l’extrait de code utilise l’approche de l’authentification interactive.</span><span class="sxs-lookup"><span data-stu-id="e2148-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="e2148-263">Authentifier des applications de manière non interactive à l’aide d’Azure Active Directory avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="e2148-264">Consultez [Créer des applications HDInsight d’authentification non interactives](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="e2148-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="e2148-265">Envoyer une tâche Hive à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="e2148-266">Consulter [Envoi de tâches Hive](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="e2148-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e2148-267">Envoyer une tâche Pig à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="e2148-268">Consulter [Envoi de tâches Pig](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="e2148-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e2148-269">Envoyer une tâche Sqoop à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="e2148-270">Consulter [Envoi de tâches Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="e2148-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="e2148-271">Répertorier les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-272">Consulter [Répertorier les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="e2148-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="e2148-273">Mettre à l’échelle les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-274">Consulter [Mettre à l’échelle les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="e2148-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="e2148-275">Autoriser/révoquer l’accès aux clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-276">Consulter [Autoriser/révoquer l’accès aux clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="e2148-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="e2148-277">Mettre à jour les informations d’identification de l’utilisateur HTTP pour les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-278">Consulter [Mettre à jour les informations d’identification de l’utilisateur HTTP pour les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="e2148-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="e2148-279">Rechercher le compte de stockage par défaut pour les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-280">Consulter [Rechercher le compte de stockage par défaut pour les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="e2148-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="e2148-281">Supprimer des clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e2148-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="e2148-282">Consulter [Supprimer des clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="e2148-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="e2148-283">Exemples</span><span class="sxs-lookup"><span data-stu-id="e2148-283">Examples</span></span>
<span data-ttu-id="e2148-284">Vous trouverez ci-dessous des exemples de la façon dont une opération est effectuée à l’aide du Kit de développement logiciel (SDK) ASM et de l’extrait de code équivalent pour le SDK ARM.</span><span class="sxs-lookup"><span data-stu-id="e2148-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="e2148-285">**Création d’un client CRUD de cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="e2148-286">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="e2148-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="e2148-287">Nouvelle commande (ARM) (autorisation du principal de service)</span><span class="sxs-lookup"><span data-stu-id="e2148-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="e2148-288">Nouvelle commande (ARM) (autorisation de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="e2148-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="e2148-289">**Création d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-289">**Creating a cluster**</span></span>

* <span data-ttu-id="e2148-290">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="e2148-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="e2148-291">Nouvelle commande (ARM)</span><span class="sxs-lookup"><span data-stu-id="e2148-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="e2148-292">**Activation de l’accès HTTP**</span><span class="sxs-lookup"><span data-stu-id="e2148-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="e2148-293">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="e2148-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="e2148-294">Nouvelle commande (ARM)</span><span class="sxs-lookup"><span data-stu-id="e2148-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="e2148-295">**Suppression d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="e2148-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="e2148-296">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="e2148-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="e2148-297">Nouvelle commande (ARM)</span><span class="sxs-lookup"><span data-stu-id="e2148-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

