---
title: Utiliser MapReduce et PowerShell avec Hadoop - Azure | Documents Microsoft
description: "Apprenez à utiliser PowerShell pour exécuter des tâches MapReduce à distance avec Hadoop sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="2e010-103">Exécution à distance des travaux MapReduce avec Hadoop sur HDInsight à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e010-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="2e010-104">Ce document fournit un exemple d’utilisation d’Azure PowerShell pour exécuter une tâche MapReduce sur un Hadoop sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e010-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="2e010-105"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="2e010-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="2e010-106">**Un cluster Azure HDInsight (Hadoop sur HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="2e010-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2e010-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="2e010-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2e010-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2e010-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="2e010-109">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2e010-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="2e010-110"><a id="powershell"></a>Exécution d’une tâche MapReduce avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e010-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="2e010-111">Azure PowerShell propose des *applets de commande* qui vous permettent d'exécuter à distance des tâches MapReduce sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e010-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="2e010-112">En interne, cela est accompli en effectuant des appels REST à [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anciennement nommé Templeton) exécuté sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e010-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="2e010-113">Les applets de commande suivantes sont utilisées lors de l’exécution des tâches MapReduce sur un cluster HDInsight à distance.</span><span class="sxs-lookup"><span data-stu-id="2e010-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="2e010-114">**Login-AzureRmAccount** : authentifie Azure PowerShell sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2e010-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="2e010-115">**New-AzureRmHDInsightMapReduceJobDefinition** : crée une *définition de tâche* avec les informations MapReduce spécifiées.</span><span class="sxs-lookup"><span data-stu-id="2e010-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="2e010-116">**Start-AzureRmHDInsightJob** : envoie la définition de la tâche à HDInsight, lance la tâche et retourne un objet de *tâche* pouvant être utilisé pour vérifier l’état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2e010-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="2e010-117">**Wait-AzureRmHDInsightJob**: utilise l’objet de la tâche pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2e010-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="2e010-118">Il attend que la tâche soit terminée ou que le délai d’attente soit dépassé.</span><span class="sxs-lookup"><span data-stu-id="2e010-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="2e010-119">**Get-AzureRmHDInsightJobOutput** : permet de récupérer la sortie de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2e010-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="2e010-120">Les étapes suivantes montrent comment utiliser ces applets de commande pour exécuter une tâche sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e010-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="2e010-121">À l’aide d’un éditeur, enregistrez le code suivant sous **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="2e010-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="2e010-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="2e010-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="2e010-123">Ouvrez une invite de commandes **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="2e010-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="2e010-124">Accédez à l’emplacement du fichier **mapreducejob.ps1** , puis utilisez les éléments suivants pour exécuter le script :</span><span class="sxs-lookup"><span data-stu-id="2e010-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="2e010-125">Lorsque vous exécutez le script, vous êtes invité à entrer le nom du cluster HDInsight et le nom du compte HTTPS/Admin, ainsi que le mot de passe pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="2e010-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="2e010-126">Vous pouvez également être invité à vous authentifier sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2e010-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="2e010-127">Une fois la tâche terminée, vous obtenez un résultat similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="2e010-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="2e010-128">Cela indique que la tâche a été effectuée avec succès.</span><span class="sxs-lookup"><span data-stu-id="2e010-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2e010-129">Si **ExitCode** correspond à une valeur différente de 0, consultez [Dépannage](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="2e010-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="2e010-130">Cet exemple stocke également les fichiers téléchargés dans un dossier **output.txt** dans le répertoire à partir duquel vous avez exécuté le script.</span><span class="sxs-lookup"><span data-stu-id="2e010-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="2e010-131">Affichage de la sortie</span><span class="sxs-lookup"><span data-stu-id="2e010-131">View output</span></span>

<span data-ttu-id="2e010-132">Ouvrez le fichier **output.txt** dans un éditeur de texte pour afficher les mots et les décomptes générés par la tâche.</span><span class="sxs-lookup"><span data-stu-id="2e010-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="2e010-133">Les fichiers de résultat d’une tâche MapReduce sont immuables.</span><span class="sxs-lookup"><span data-stu-id="2e010-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="2e010-134">Donc, si vous réexécutez cet exemple, vous devez modifier le nom du fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="2e010-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="2e010-135"><a id="troubleshooting"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="2e010-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="2e010-136">Si aucune information n'est retournée lorsque la tâche est terminée, il se peut qu'une erreur soit survenue au cours du traitement.</span><span class="sxs-lookup"><span data-stu-id="2e010-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="2e010-137">Pour afficher les informations d’erreur pour ce projet, ajoutez la commande suivante à la fin du fichier **mapreducejob.ps1** , enregistrez-le et exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="2e010-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="2e010-138">Cette applet de commande renvoie les informations écrites dans STDERR sur le serveur lors de l’exécution de la tâche et peut vous aider à déterminer pourquoi la tâche échoue.</span><span class="sxs-lookup"><span data-stu-id="2e010-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="2e010-139"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="2e010-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="2e010-140">Comme vous pouvez le voir, Azure PowerShell offre un moyen facile d’exécuter des tâches MapReduce sur un cluster HDInsight, de surveiller l’état de la tâche et de récupérer la sortie.</span><span class="sxs-lookup"><span data-stu-id="2e010-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="2e010-141"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e010-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2e010-142">Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2e010-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="2e010-143">Utilisation de MapReduce dans Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e010-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="2e010-144">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="2e010-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2e010-145">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e010-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2e010-146">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e010-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
