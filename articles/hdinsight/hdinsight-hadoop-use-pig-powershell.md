---
title: "Utiliser Hadoop Pig avec PowerShell dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment soumettre des tâches Pig vers un cluster Hadoop sur HDInsight à l’aide d’Azure Powershell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="aaf4d-103">Utilisation d’Azure PowerShell pour exécuter des tâches Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="aaf4d-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="aaf4d-104">Ce document fournit un exemple d’utilisation d’Azure PowerShell pour soumettre des tâches Pig à un Hadoop sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="aaf4d-105">Pig vous permet d’écrire des tâches MapReduce en utilisant un langage (Pig Latin) qui modélise les transformations de données, plutôt que de mapper et de réduire les fonctions.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="aaf4d-106">Ce document ne fournit pas une description détaillée de ce que font les instructions Pig Latin utilisées dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="aaf4d-107">Pour plus d’informations sur le langage Pig Latin utilisé dans cet exemple, consultez la rubrique [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="aaf4d-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="aaf4d-108"><a id="prereq"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="aaf4d-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="aaf4d-109">**Un cluster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="aaf4d-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="aaf4d-110">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aaf4d-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aaf4d-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="aaf4d-112">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="aaf4d-113"><a id="powershell"></a>Exécution de tâches Pig avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaf4d-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="aaf4d-114">Azure PowerShell propose des *applets de commande* qui vous permettent d'exécuter à distance des tâches Pig sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="aaf4d-115">En interne, PowerShell utilise des appels REST vers [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) en cours d’exécution sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="aaf4d-116">Les applets de commande suivantes sont utilisées lors de l’exécution des tâches Pig sur un cluster HDInsight à distance :</span><span class="sxs-lookup"><span data-stu-id="aaf4d-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="aaf4d-117">**Login-AzureRmAccount**: authentifie Azure PowerShell sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="aaf4d-118">**New-AzureRmHDInsightPigJobDefinition**: crée une *définition d’une tâche* à l’aide des instructions Pig Latin spécifiées</span><span class="sxs-lookup"><span data-stu-id="aaf4d-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="aaf4d-119">**Start-AzureRmHDInsightJob**: envoie la définition de la tâche à HDInsight, démarre la tâche et retourne un objet de *tâche* pouvant être utilisé pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="aaf4d-120">**Wait-AzureRmHDInsightJob**: utilise l’objet de la tâche pour vérifier le statut de la tâche.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="aaf4d-121">Il attend que la tâche soit terminée ou que le délai d’attente soit dépassé.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="aaf4d-122">**Get-AzureRmHDInsightJobOutput**: utilisé pour récupérer la sortie de la tâche.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="aaf4d-123">Les étapes suivantes montrent comment utiliser ces cmdlets pour exécuter une tâche sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="aaf4d-124">À l’aide d’un éditeur, enregistrez le code suivant sous **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="aaf4d-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="aaf4d-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="aaf4d-126">Ouvrez une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="aaf4d-127">Accédez au répertoire du fichier **pigjob.ps1** , puis utilisez la commande suivante pour exécuter le script :</span><span class="sxs-lookup"><span data-stu-id="aaf4d-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="aaf4d-128">Vous êtes invité à vous connecter à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="aaf4d-129">Ensuite, vous devez fournir le nom et le mot de passe du compte HTTPs/Admin pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="aaf4d-130">Une fois la tâche terminée, un texte similaire à celui présenté ci-dessous doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="aaf4d-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="aaf4d-131"><a id="troubleshooting"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="aaf4d-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="aaf4d-132">Si aucune information n'est retournée lorsque la tâche est terminée, il se peut qu'une erreur soit survenue au cours du traitement.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="aaf4d-133">Pour afficher les informations d’erreur pour cette tâche, ajoutez la commande suivante à la fin du fichier **pigjob.ps1** , enregistrez-le et exécutez-le à nouveau.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="aaf4d-134">Cela renvoie les informations écrites dans STDERR sur le serveur lors de l’exécution de la tâche et peut vous aider à déterminer pourquoi la tâche échoue.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="aaf4d-135"><a id="summary"></a>Résumé</span><span class="sxs-lookup"><span data-stu-id="aaf4d-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="aaf4d-136">Comme vous pouvez le voir, Azure PowerShell offre un moyen facile d’exécuter des tâches Pig sur un cluster HDInsight, de surveiller l’état de la tâche et de récupérer la sortie.</span><span class="sxs-lookup"><span data-stu-id="aaf4d-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="aaf4d-137"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aaf4d-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="aaf4d-138">Pour obtenir des informations générales sur Pig dans HDInsight :</span><span class="sxs-lookup"><span data-stu-id="aaf4d-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="aaf4d-139">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="aaf4d-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="aaf4d-140">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="aaf4d-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="aaf4d-141">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="aaf4d-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="aaf4d-142">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="aaf4d-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
