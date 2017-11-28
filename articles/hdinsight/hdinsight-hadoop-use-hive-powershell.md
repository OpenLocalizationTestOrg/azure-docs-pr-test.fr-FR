---
title: "Utiliser Hadoop Hive avec PowerShell dans HDInsight - Azure | Documents Microsoft"
description: "Utilisez PowerShell pour exécuter des requêtes Hive dans Hadoop sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="0dda2-103">Exécution de requêtes Hive avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dda2-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="0dda2-104">Ce document fournit un exemple d’utilisation d’Azure PowerShell dans le mode Groupe de ressources Azure pour exécuter des requêtes Hive sur un cluster Hadoop sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0dda2-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="0dda2-105">Ce document ne fournit pas de description détaillée de ce que font les instructions HiveQL utilisées dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="0dda2-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="0dda2-106">Pour plus d’informations sur le langage HiveQL utilisé dans cet exemple, consultez la page [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="0dda2-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="0dda2-107">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="0dda2-107">**Prerequisites**</span></span>

* <span data-ttu-id="0dda2-108">**Un cluster Azure HDInsight** : peu importe si le cluster est basé sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="0dda2-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0dda2-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="0dda2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0dda2-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0dda2-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0dda2-111">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0dda2-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="0dda2-112">Exécution de requêtes Hive avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dda2-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="0dda2-113">Azure PowerShell fournit des *cmdlets* qui vous permettent d'exécuter à distance des requêtes Hive sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0dda2-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="0dda2-114">En interne, les applets de commande effectuent des appels REST à [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0dda2-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="0dda2-115">Les applets de commande suivants sont utilisés lors de l'exécution de requêtes Hive sur un cluster à distance HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0dda2-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="0dda2-116">**Add-AzureRmAccount**: authentifie Azure PowerShell dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0dda2-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="0dda2-117">**New-AzureRmHDInsightHiveJobDefinition** : crée une *définition de travail* à l’aide des instructions HiveQL spécifiées.</span><span class="sxs-lookup"><span data-stu-id="0dda2-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="0dda2-118">**Start-AzureRmHDInsightJob**: envoie la définition de la tâche à HDInsight, démarre la tâche et retourne un objet de *tâche* pouvant être utilisé pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="0dda2-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="0dda2-119">**Wait-AzureRmHDInsightJob**: utilise l’objet de la tâche pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="0dda2-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="0dda2-120">Il attend que la tâche soit terminée ou que le délai d’attente soit dépassé.</span><span class="sxs-lookup"><span data-stu-id="0dda2-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="0dda2-121">**Get-AzureRmHDInsightJobOutput**: utilisé pour récupérer la sortie de la tâche.</span><span class="sxs-lookup"><span data-stu-id="0dda2-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="0dda2-122">**Invoke-AzureRmHDInsightHiveJob**: utilisé pour exécuter des instructions HiveQL.</span><span class="sxs-lookup"><span data-stu-id="0dda2-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="0dda2-123">Cette applet de commande bloque la fin de la requête, puis retourne les résultats.</span><span class="sxs-lookup"><span data-stu-id="0dda2-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="0dda2-124">**Use-AzureRmHDInsightCluster** : configure le cluster actuel à utiliser pour la commande **Invoke-AzureRmHDInsightHiveJob**</span><span class="sxs-lookup"><span data-stu-id="0dda2-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="0dda2-125">Les étapes suivantes montrent comment utiliser ces cmdlets pour exécuter une tâche sur votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0dda2-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="0dda2-126">À l'aide d'un éditeur, enregistrez le code suivant en tant que **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="0dda2-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="0dda2-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="0dda2-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="0dda2-128">Ouvrez une invite de commandes **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="0dda2-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="0dda2-129">Accédez au répertoire du fichier **hivejob.ps1** , puis utilisez la commande suivante pour exécuter le script :</span><span class="sxs-lookup"><span data-stu-id="0dda2-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="0dda2-130">Quand le script s’exécute, vous devez entrer le nom du cluster et les informations d’identification du compte HTTPS/Admin pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="0dda2-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="0dda2-131">Vous pouvez également être invité à vous connecter à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0dda2-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="0dda2-132">Une fois la tâche terminée, des informations similaires à celles présentées ci-dessous s’affichent :</span><span class="sxs-lookup"><span data-stu-id="0dda2-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="0dda2-133">Comme mentionné précédemment, **Invoke-Hive** peut être utilisé pour exécuter une requête et attendre la réponse.</span><span class="sxs-lookup"><span data-stu-id="0dda2-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="0dda2-134">Pour voir comment fonctionne Invoke-Hive, utilisez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="0dda2-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="0dda2-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="0dda2-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="0dda2-136">La sortie ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="0dda2-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="0dda2-137">Pour les requêtes HiveQL plus longues, vous pouvez utiliser les fichiers de script HiveQL de PowerShell ou la cmdlet **Here-Strings** Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0dda2-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="0dda2-138">L'extrait suivant montre comment utiliser la cmdlet **Invoke-Hive** pour exécuter un fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="0dda2-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="0dda2-139">Ce dernier doit être chargé dans wasb://.</span><span class="sxs-lookup"><span data-stu-id="0dda2-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="0dda2-140">Pour plus d'informations sur **Here-Strings**, consultez la page <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Utilisation du fichier de script Here-Strings de PowerShell</a>.</span><span class="sxs-lookup"><span data-stu-id="0dda2-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0dda2-141">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="0dda2-141">Troubleshooting</span></span>

<span data-ttu-id="0dda2-142">Si aucune information n'est retournée lorsque la tâche est terminée, il se peut qu'une erreur soit survenue au cours du traitement.</span><span class="sxs-lookup"><span data-stu-id="0dda2-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="0dda2-143">Pour afficher les informations d'erreur relatives à cette tâche, ajoutez les commandes suivantes à la fin du fichier **hivejob.ps1** , enregistrez-le, puis exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="0dda2-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="0dda2-144">Cette applet de commande retourne les informations écrites dans STDERR sur le serveur lors de l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="0dda2-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="0dda2-145">Résumé</span><span class="sxs-lookup"><span data-stu-id="0dda2-145">Summary</span></span>

<span data-ttu-id="0dda2-146">Comme vous pouvez le constater, Azure PowerShell permet d'exécuter facilement des requêtes Hive sur un cluster HDInsight, de surveiller l'état de la tâche et de récupérer le résultat.</span><span class="sxs-lookup"><span data-stu-id="0dda2-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dda2-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0dda2-147">Next steps</span></span>

<span data-ttu-id="0dda2-148">Pour obtenir des informations générales sur Hive dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0dda2-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="0dda2-149">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="0dda2-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0dda2-150">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="0dda2-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="0dda2-151">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="0dda2-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0dda2-152">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="0dda2-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
