---
title: aaaMigrate tooAzure le Gestionnaire de ressources des outils pour HDInsight | Documents Microsoft
description: "Comment toomigrate tooAzure Gestionnaire de ressources du développement des outils pour les clusters HDInsight"
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="ec4ba-103">Outils de développement basé sur le Gestionnaire de ressources tooAzure migration pour les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec4ba-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="ec4ba-104">HDInsight déconseille les outils Azure Service Manager (ASM) pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="ec4ba-105">Si vous utilisez Azure PowerShell ou CLI d’Azure hello HDInsight .NET SDK toowork avec des clusters HDInsight, vous êtes invités toouse hello Azure Resource Manager ARM versions de PowerShell, CLI et Kit de développement .NET à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="ec4ba-106">Cet article fournit des pointeurs sur la façon de toomigrate toohello nouveau ARM approche.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="ec4ba-107">Autant que possible, cet article souligne également les différences de hello entre les approches ASM et ARM hello pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec4ba-108">prise en charge de Hello pour ASM en fonction de PowerShell, CLI, et Kit de développement .NET va interrompre son **le 1er janvier 2017**.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="ec4ba-109">Migration tooAzure CLI d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec4ba-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="ec4ba-110">Hello CLI d’Azure maintenant par défaut le mode tooAzure Resource Manager (ARM), sauf si vous mettez à niveau à partir d’une installation précédente ; Dans ce cas, vous devrez peut-être toouse hello `azure config mode arm` tooARM en mode tooswitch de commande.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="ec4ba-111">commandes de base Hello que hello CLI d’Azure fourni toowork avec HDInsight à l’aide d’Azure Service Management (ASM) hello sont identiques lors de l’utilisation de ARM ; Toutefois certains paramètres et les commutateurs peuvent avoir des nouveaux noms, et plusieurs nouveaux paramètres sont disponibles lors de l’utilisation de ARM.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="ec4ba-112">Par exemple, vous pouvez maintenant utiliser `azure hdinsight cluster create` toospecify hello réseau virtuel Azure et qui doit être créé dans un cluster, ou la ruche et les informations du magasin de métadonnées Oozie.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="ec4ba-113">Les commandes de base pour travailler avec HDInsight via le Azure Resource Manager sont :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="ec4ba-114">`azure hdinsight cluster create` - crée un nouveau cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec4ba-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="ec4ba-115">`azure hdinsight cluster delete` - supprime un cluster HDInsight existant</span><span class="sxs-lookup"><span data-stu-id="ec4ba-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="ec4ba-116">`azure hdinsight cluster show` -affiche des informations sur un cluster existant</span><span class="sxs-lookup"><span data-stu-id="ec4ba-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="ec4ba-117">`azure hdinsight cluster list` - répertorie les clusters HDInsight pour votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="ec4ba-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="ec4ba-118">Hello d’utilisation `-h` passer des paramètres de hello tooinspect et les options disponibles pour chaque commande.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="ec4ba-119">Nouvelles commandes</span><span class="sxs-lookup"><span data-stu-id="ec4ba-119">New commands</span></span>
<span data-ttu-id="ec4ba-120">Les nouvelles commandes disponibles avec Azure Resource Manager sont :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="ec4ba-121">`azure hdinsight cluster resize`-dynamiquement les modifications hello nombre de nœuds de cluster de hello travail</span><span class="sxs-lookup"><span data-stu-id="ec4ba-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="ec4ba-122">`azure hdinsight cluster enable-http-access`-permet de cluster de toohello accès HTTPs (sur par défaut)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="ec4ba-123">`azure hdinsight cluster disable-http-access`-désactive le cluster de toohello accès HTTPs</span><span class="sxs-lookup"><span data-stu-id="ec4ba-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="ec4ba-124">`azure hdinsight script-action` - fournit des commandes pour créer/gérer des actions de script sur un cluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="ec4ba-125">`azure hdinsight config`-Fournit des commandes pour la création d’un fichier de configuration qui peut être utilisé avec hello `hdinsight cluster create` tooprovide les informations de configuration de la commande.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="ec4ba-126">Commandes déconseillées</span><span class="sxs-lookup"><span data-stu-id="ec4ba-126">Deprecated commands</span></span>
<span data-ttu-id="ec4ba-127">Si vous utilisez hello `azure hdinsight job` commandes toosubmit travaux tooyour HDInsight cluster ceux-ci ne sont pas disponibles via les commandes de hello ARM.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="ec4ba-128">Si vous devez tooprogrammatically submit travaux tooHDInsight à partir de scripts, vous devez utiliser à la place hello API REST fournie par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="ec4ba-129">Pour plus d’informations sur la soumission de travaux à l’aide des API REST, consultez hello suivant des documents.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="ec4ba-130">Exécution à distance des tâches MapReduce avec Hadoop sur HDInsight à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="ec4ba-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="ec4ba-131">Exécution de requêtes Hive avec Hadoop dans HDInsight via Curl</span><span class="sxs-lookup"><span data-stu-id="ec4ba-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="ec4ba-132">Exécution à distance des tâches Pig avec Hadoop sur HDInsight à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="ec4ba-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="ec4ba-133">Pour plus d’informations sur les autres façons de toorun MapReduce, Hive, porc de manière interactive, consultez [MapReduce utilisation avec Hadoop dans HDInsight](hdinsight-use-mapreduce.md), [utilisez Hive avec Hadoop dans HDInsight](hdinsight-use-hive.md), et [utilisez Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="ec4ba-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="ec4ba-134">Examples</span></span>
<span data-ttu-id="ec4ba-135">**Création d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-135">**Creating a cluster**</span></span>

* <span data-ttu-id="ec4ba-136">Ancienne commande (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="ec4ba-137">Nouvelle commande (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="ec4ba-138">**Suppression d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="ec4ba-139">Ancienne commande (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="ec4ba-140">Nouvelle commande (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="ec4ba-141">**Énumérer les clusters**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-141">**List clusters**</span></span>

* <span data-ttu-id="ec4ba-142">Ancienne commande (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="ec4ba-143">Nouvelle commande (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="ec4ba-144">Pour la commande liste hello spécifiant hello le groupe de ressources à l’aide `-g` retourne uniquement les clusters hello dans le groupe de ressources spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="ec4ba-145">**Afficher les informations du cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-145">**Show cluster information**</span></span>

* <span data-ttu-id="ec4ba-146">Ancienne commande (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="ec4ba-147">Nouvelle commande (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="ec4ba-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="ec4ba-148">Migration Azure PowerShell tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="ec4ba-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="ec4ba-149">Hello des informations générales sur Azure PowerShell en mode Azure Resource Manager (ARM) de hello trouverez [à l’aide de Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="ec4ba-150">Hello applets de commande Azure PowerShell ARM peut être installé côte à côte avec hello ASM applets de commande.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="ec4ba-151">applets de commande Hello à partir des deux modes de hello peuvent être distingués par leurs noms.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="ec4ba-152">le mode Hello ARM a *AzureRmHDInsight* dans les noms d’applet de commande hello comparaison trop*AzureHDInsight* en mode ASM hello.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="ec4ba-153">Par exemple, *New-AzureRmHDInsightCluster* et *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="ec4ba-154">Toutefois, certains paramètres et commutateurs peuvent avoir des nouveaux noms, et de nombreux nouveaux paramètres sont disponibles lorsque vous utilisez ARM.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="ec4ba-155">Par exemple, plusieurs applets de commande exigent un nouveau commutateur appelé *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="ec4ba-156">Avant de pouvoir utiliser les applets de commande HDInsight hello, vous devez vous connecter tooyour compte Azure et créer un nouveau groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="ec4ba-157">Login-AzureRmAccount ou [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="ec4ba-158">Consultez [Authentification d’un principal du service à l’aide d’Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="ec4ba-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ec4ba-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="ec4ba-160">Applets de commande renommées</span><span class="sxs-lookup"><span data-stu-id="ec4ba-160">Renamed cmdlets</span></span>
<span data-ttu-id="ec4ba-161">hello toolist HDInsight ASM des applets de commande dans la console Windows PowerShell :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="ec4ba-162">Hello tableau suivant répertorie hello ASM applets de commande et leurs noms dans le mode hello ARM :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="ec4ba-163">Applets de commande ASM</span><span class="sxs-lookup"><span data-stu-id="ec4ba-163">ASM cmdlets</span></span> | <span data-ttu-id="ec4ba-164">Applets de commande ARM</span><span class="sxs-lookup"><span data-stu-id="ec4ba-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="ec4ba-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="ec4ba-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="ec4ba-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="ec4ba-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="ec4ba-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="ec4ba-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="ec4ba-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="ec4ba-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="ec4ba-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="ec4ba-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="ec4ba-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="ec4ba-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="ec4ba-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="ec4ba-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="ec4ba-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="ec4ba-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="ec4ba-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="ec4ba-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="ec4ba-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="ec4ba-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="ec4ba-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="ec4ba-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="ec4ba-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="ec4ba-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="ec4ba-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="ec4ba-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="ec4ba-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="ec4ba-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="ec4ba-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="ec4ba-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="ec4ba-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="ec4ba-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="ec4ba-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="ec4ba-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="ec4ba-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="ec4ba-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="ec4ba-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="ec4ba-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="ec4ba-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="ec4ba-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="ec4ba-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="ec4ba-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="ec4ba-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="ec4ba-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="ec4ba-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="ec4ba-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="ec4ba-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="ec4ba-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="ec4ba-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="ec4ba-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="ec4ba-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="ec4ba-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="ec4ba-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="ec4ba-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="ec4ba-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="ec4ba-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="ec4ba-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="ec4ba-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="ec4ba-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="ec4ba-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="ec4ba-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="ec4ba-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="ec4ba-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="ec4ba-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="ec4ba-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="ec4ba-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="ec4ba-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="ec4ba-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="ec4ba-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="ec4ba-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="ec4ba-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="ec4ba-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="ec4ba-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="ec4ba-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="ec4ba-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="ec4ba-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="ec4ba-219">Nouvelles applets de commande</span><span class="sxs-lookup"><span data-stu-id="ec4ba-219">New cmdlets</span></span>
<span data-ttu-id="ec4ba-220">Hello Voici hello nouvelles applets de commande qui sont disponibles uniquement dans le mode hello ARM.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="ec4ba-221">**Applets de commandes associées à une action de script :**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="ec4ba-222">**Get-AzureRmHDInsightPersistedScriptAction**: Obtient hello persistante des actions de script pour un cluster et les répertorie dans l’ordre chronologique ou obtient les détails d’une action de script persistantes spécifié.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="ec4ba-223">**Get-AzureRmHDInsightScriptActionHistory**: Obtient l’historique des actions de script hello pour un cluster et répertorie dans l’ordre chronologique inverse ou obtient les détails d’une action de script exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="ec4ba-224">**Remove-AzureRmHDInsightPersistedScriptAction**: retire une action de script persistante d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="ec4ba-225">**Set-AzureRmHDInsightPersistedScriptAction**: définit un toobe d’action de script précédemment exécuté une action de script persistantes.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="ec4ba-226">**AzureRmHDInsightScriptAction envoyer**: soumet un cluster Azure HDInsight tooan de nouveau script action.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="ec4ba-227">Pour plus d’informations sur l’utilisation, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="ec4ba-228">**Applets de commande associées à l’identité du cluster :**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="ec4ba-229">**AzureRmHDInsightClusterIdentity ajouter**: ajoute un objet de configuration de cluster identité tooa cluster afin que hello cluster HDInsight peut accéder aux magasins de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="ec4ba-230">Consultez la page [Créer un cluster HDInsight avec Data Lake Store à l’aide d’Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="ec4ba-231">Exemples</span><span class="sxs-lookup"><span data-stu-id="ec4ba-231">Examples</span></span>
<span data-ttu-id="ec4ba-232">**Créer un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-232">**Create cluster**</span></span>

<span data-ttu-id="ec4ba-233">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="ec4ba-234">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-234">New command (ARM):</span></span>

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


<span data-ttu-id="ec4ba-235">**Supprimer un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-235">**Delete cluster**</span></span>

<span data-ttu-id="ec4ba-236">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="ec4ba-237">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="ec4ba-238">**Répertorier un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-238">**List cluster**</span></span>

<span data-ttu-id="ec4ba-239">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="ec4ba-240">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="ec4ba-241">**Afficher le cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-241">**Show cluster**</span></span>

<span data-ttu-id="ec4ba-242">Ancienne commande (ASM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="ec4ba-243">Nouvelle commande (ARM) :</span><span class="sxs-lookup"><span data-stu-id="ec4ba-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="ec4ba-244">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="ec4ba-244">Other samples</span></span>
* [<span data-ttu-id="ec4ba-245">Création de clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec4ba-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="ec4ba-246">Envoi de tâches Hive</span><span class="sxs-lookup"><span data-stu-id="ec4ba-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="ec4ba-247">Envoi de tâches Pig</span><span class="sxs-lookup"><span data-stu-id="ec4ba-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="ec4ba-248">Envoi de tâches Sqoop</span><span class="sxs-lookup"><span data-stu-id="ec4ba-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="ec4ba-249">Migration toohello basés sur ARM HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ec4ba-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="ec4ba-250">Hello basée sur la gestion des services Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) est désormais déconseillée.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="ec4ba-251">Vous êtes invité toouse hello basée sur la gestion des ressources Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="ec4ba-252">Hello packages HDInsight de base ASM suivants sont déconseillés.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="ec4ba-253">Cette section fournit des pointeurs toomore plus d’informations sur la façon de tooperform certaine tâches à l’aide de hello basés sur ARM Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="ec4ba-254">Comment... à l’aide de hello basés sur ARM des SDK HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec4ba-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="ec4ba-255">Liens</span><span class="sxs-lookup"><span data-stu-id="ec4ba-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="ec4ba-256">Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-257">Consultez [Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="ec4ba-258">Personnaliser un cluster à l’aide d’une action de script avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="ec4ba-259">Consultez [Personnaliser des clusters HDInsight sous Linux à l’aide d’une action de script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="ec4ba-260">Authentifier des applications de manière interactive à l’aide d’Azure Active Directory avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="ec4ba-261">Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ec4ba-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="ec4ba-262">extrait de code Hello dans cet article utilise l’approche de l’authentification interactive hello.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="ec4ba-263">Authentifier des applications de manière non interactive à l’aide d’Azure Active Directory avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="ec4ba-264">Consultez [Créer des applications HDInsight d’authentification non interactives](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="ec4ba-265">Envoyer une tâche Hive à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="ec4ba-266">Consulter [Envoi de tâches Hive](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="ec4ba-267">Envoyer une tâche Pig à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="ec4ba-268">Consulter [Envoi de tâches Pig](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="ec4ba-269">Envoyer une tâche Sqoop à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="ec4ba-270">Consulter [Envoi de tâches Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="ec4ba-271">Répertorier les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-272">Consulter [Répertorier les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="ec4ba-273">Mettre à l’échelle les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-274">Consulter [Mettre à l’échelle les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="ec4ba-275">Autorisations GRANT/revoke accès tooHDInsight clusters à l’aide du Kit de développement .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-276">Consultez [clusters de tooHDInsight accès Grant/revoke.](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="ec4ba-277">Mettre à jour les informations d’identification de l’utilisateur HTTP pour les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-278">Consulter [Mettre à jour les informations d’identification de l’utilisateur HTTP pour les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="ec4ba-279">Rechercher le compte de stockage par défaut hello pour les clusters HDInsight à l’aide du Kit de développement .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-280">Consultez [trouver le compte de stockage par défaut hello pour les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="ec4ba-281">Supprimer des clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ec4ba-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="ec4ba-282">Consulter [Supprimer des clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="ec4ba-283">Exemples</span><span class="sxs-lookup"><span data-stu-id="ec4ba-283">Examples</span></span>
<span data-ttu-id="ec4ba-284">Voici quelques exemples sur la façon dont une opération est effectuée à l’aide de hello basée sur ASM Kit de développement logiciel et extrait de code équivalent hello pour hello basés sur ARM Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="ec4ba-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="ec4ba-285">**Création d’un client CRUD de cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="ec4ba-286">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="ec4ba-287">Nouvelle commande (ARM) (autorisation du principal de service)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="ec4ba-288">Nouvelle commande (ARM) (autorisation de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="ec4ba-289">**Création d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-289">**Creating a cluster**</span></span>

* <span data-ttu-id="ec4ba-290">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="ec4ba-291">Nouvelle commande (ARM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="ec4ba-292">**Activation de l’accès HTTP**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="ec4ba-293">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="ec4ba-294">Nouvelle commande (ARM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="ec4ba-295">**Suppression d’un cluster**</span><span class="sxs-lookup"><span data-stu-id="ec4ba-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="ec4ba-296">Ancienne commande (ASM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="ec4ba-297">Nouvelle commande (ARM)</span><span class="sxs-lookup"><span data-stu-id="ec4ba-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

